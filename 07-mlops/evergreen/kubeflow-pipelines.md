---
title: Kubeflow Pipelines
type: evergreen
domain: mlops
status: seed
visibility: PORTFOLIO_SAFE
rag_ready: true
created: 2026-05-27
last_updated: 2026-05-27
tags:
  - mlops
  - kubeflow
  - orchestration
  - kubernetes
  - pipelines
  - aws
  - quantpath
aliases:
  - KFP
  - Kubeflow Pipelines v2
  - ML pipeline orchestration
  - Kubernetes ML pipelines
---

# Kubeflow Pipelines

**Summary**: A platform for building, deploying, and managing portable, scalable ML workflows on Kubernetes — where each pipeline step runs as an isolated container with explicit inputs, outputs, and dependency declarations, enabling reproducible and auditable ML experimentation at scale.

**Type**: Evergreen note
**Domain**: MLOps / Orchestration / Infrastructure
**Status**: Seed
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2026-05-27

---

## Core Concept

Kubeflow Pipelines (KFP) treats ML workflows as directed acyclic graphs (DAGs) of containerized steps. Each step:
- Runs in its own container (isolation)
- Declares typed inputs and outputs (contracts)
- Produces artifacts with metadata (lineage)
- Can be cached, retried, and conditionally executed

This is the antithesis of monolithic notebook execution. Instead of "run all cells top to bottom," KFP enforces:
- **Explicit dependencies** between steps
- **Reproducible environments** per step (containers)
- **Artifact tracking** for every intermediate output
- **Parallelism** where the DAG allows it

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    Kubeflow Pipelines Stack                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                   │
│  Pipeline Definition (Python SDK)                                 │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │  @dsl.pipeline                                             │  │
│  │  def training_pipeline(data_path, epochs):                 │  │
│  │      preprocess = preprocess_op(data_path)                 │  │
│  │      train = train_op(preprocess.output, epochs)           │  │
│  │      evaluate = evaluate_op(train.output)                  │  │
│  └───────────────────────────────────────────────────────────┘  │
│                              │                                    │
│                              ▼                                    │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │  Pipeline Compiler → IR YAML                               │  │
│  └───────────────────────────────────────────────────────────┘  │
│                              │                                    │
│                              ▼                                    │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │  Pipeline Service (API Server)                             │  │
│  │  - Run management                                          │  │
│  │  - Scheduling                                              │  │
│  │  - Artifact/metadata store                                 │  │
│  └───────────────────────────────────────────────────────────┘  │
│                              │                                    │
│                              ▼                                    │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │  Kubernetes (Argo Workflows / Tekton)                      │  │
│  │  - Pod scheduling                                          │  │
│  │  - Resource allocation                                     │  │
│  │  - Container execution                                     │  │
│  └───────────────────────────────────────────────────────────┘  │
│                                                                   │
└─────────────────────────────────────────────────────────────────┘
```

---

## KFP v2 Key Concepts

### Components
Self-contained units of work with typed I/O:
```python
@dsl.component(base_image="python:3.11")
def preprocess(
    raw_data: Input[Dataset],
    processed_data: Output[Dataset],
    sample_rate: float = 0.1,
):
    import pandas as pd
    df = pd.read_parquet(raw_data.path)
    sampled = df.sample(frac=sample_rate)
    sampled.to_parquet(processed_data.path)
```

### Pipelines
DAGs composed of component invocations:
```python
@dsl.pipeline(name="training-pipeline")
def training_pipeline(data_uri: str, epochs: int = 10):
    preprocess_task = preprocess(raw_data=data_uri)
    train_task = train_model(
        data=preprocess_task.outputs["processed_data"],
        epochs=epochs,
    )
    evaluate_task = evaluate(model=train_task.outputs["model"])
```

### Artifacts
Typed intermediate outputs with automatic metadata:
- `Dataset`, `Model`, `Metrics`, `Markdown`, `HTML`
- Stored in object storage (S3, GCS, MinIO)
- Tracked in ML Metadata (MLMD) for lineage

### Caching
- Deterministic cache keys based on component code + inputs
- Unchanged steps are skipped on re-runs
- Dramatically speeds up iterative development

---

## Why This Matters in Production

1. **Reproducibility**: Every run is a fully specified execution graph with pinned containers and logged artifacts.
2. **Scalability**: Kubernetes-native scheduling enables GPU allocation, distributed training, and autoscaling.
3. **Portability**: Same pipeline definition runs on any Kubernetes cluster (cloud-agnostic).
4. **Debuggability**: Failed steps can be inspected independently; logs, artifacts, and metadata are preserved.
5. **Collaboration**: Pipelines are shareable, versionable, and composable — teams build on each other's components.
6. **Auditability**: Complete execution history with all parameters, artifacts, and outcomes recorded.

---

## Failure Modes and Risks

| Failure Mode | Impact | Mitigation |
|---|---|---|
| Container image drift | Pipeline works locally, fails in cluster | Pin image digests, use private registry |
| Resource exhaustion | OOMKill on training steps | Right-size resource requests, node auto-scaling |
| Artifact store unavailable | Pipeline hangs on I/O | Health checks, retry policies, circuit breakers |
| DAG complexity explosion | Unmaintainable spaghetti pipelines | Modular sub-pipelines, clear naming conventions |
| Cache invalidation bugs | Stale results served for changed logic | Hash-based keys including code content |
| Kubernetes version skew | Breaking API changes | Version pinning, staged cluster upgrades |
| Long-running step failures | Hours of compute wasted on late failure | Checkpointing, early validation steps |

---

## Governance Considerations

- **Pipeline versioning**: Every pipeline definition is version-controlled; deployments reference specific versions.
- **Access control**: RBAC on Kubernetes namespaces limits who can trigger production pipelines.
- **Resource quotas**: Prevent runaway pipelines from consuming cluster resources.
- **Data access governance**: Pipeline service accounts have minimal permissions scoped to required data.
- **Execution audit**: Every run produces an immutable record of what ran, with what parameters, producing what artifacts.
- **Approval gates**: Inject human approval steps before production model deployment.

---

## AWS Relevance

- **EKS (Elastic Kubernetes Service)**: Managed Kubernetes for running Kubeflow
- **SageMaker Pipelines**: AWS-managed alternative to KFP with similar DAG semantics
- **S3**: Artifact store for pipeline outputs
- **ECR**: Container registry for pipeline step images
- **IAM Roles for Service Accounts (IRSA)**: Fine-grained AWS permissions per pipeline step
- **AWS Batch**: Alternative execution backend for non-Kubernetes teams

## Databricks Relevance

- **Databricks Workflows**: Managed alternative with notebook/JAR/Python task types
- **Delta Lake**: Shared artifact layer between pipeline steps
- **MLflow integration**: Pipeline steps log to MLflow experiment tracking
- **Comparison**: KFP = container-native, portable; Databricks Workflows = managed, integrated, simpler
- **Hybrid patterns**: KFP orchestrates, Databricks executes compute-heavy steps via API

---

## Comparison with Alternatives

| Feature | Kubeflow Pipelines | Airflow | SageMaker Pipelines | Databricks Workflows |
|---|---|---|---|---|
| ML-native | Yes | No (general-purpose) | Yes | Partially |
| Container isolation | Per-step | Optional | Per-step | Cluster-level |
| Artifact tracking | Built-in (MLMD) | External | Built-in | MLflow |
| Kubernetes-native | Yes | Optional | No | No |
| Managed offering | Vertex AI (GCP) | MWAA (AWS) | Yes | Yes |
| Learning curve | High | Medium | Medium | Low |

---

## Portfolio / Project Integration Opportunities

- **QuantPath retraining pipeline**: Orchestrate data refresh → feature computation → model training → validation → deployment
- **Bedrock RAG ingestion**: Pipeline for document processing → embedding → index update → quality validation
- **Multi-model workflows**: Chain rate-regime classifier → affordability model → alert generation
- **Learning lab**: Deploy local Kubeflow on Minikube for portfolio demonstrations

---

## Related Notes

- [[ci-cd-for-ml]] — pipelines triggered and validated by CI/CD
- [[docker-layer-caching]] — container build optimization for pipeline steps
- [[mlflow-model-registry]] — pipeline outputs registered as model versions
- [[feature-store-patterns]] — pipeline steps compute and publish features
- [[observability-for-ml-systems]] — monitoring pipeline health and performance
- [[moc-mlops]] — MLOps knowledge map

---

## Sources and Further Reading

- Kubeflow Pipelines Documentation (v2)
- Google: Vertex AI Pipelines (managed KFP)
- Argo Workflows: Kubernetes-native workflow engine
- AWS: Step Functions for ML (alternative orchestration)
