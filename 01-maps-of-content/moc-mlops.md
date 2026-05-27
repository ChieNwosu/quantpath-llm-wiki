# MLOps Knowledge Map

**Purpose**: Navigation hub and conceptual index for all MLOps, production ML, and AI infrastructure knowledge in the QuantPath Learning OS.
**Status**: Active
**Last updated**: 2026-05-27
**Visibility**: PORTFOLIO_SAFE

---

## Design Philosophy

This knowledge layer approaches MLOps as **production systems engineering for machine learning** — not as a tooling checklist. Notes prioritize:
- Systems thinking over tool tutorials
- Failure modes over happy paths
- Governance over speed
- Observability over blind deployment
- Reproducibility over convenience

---

## Evergreen Notes — Core Concepts

### Model Lifecycle
- [[mlflow-model-registry]] — versioning, lineage, and governance for model artifacts
- [[model-drift-monitoring]] — detecting when deployed models degrade

### Infrastructure & Build
- [[docker-layer-caching]] — container build optimization for ML workloads
- [[kubeflow-pipelines]] — containerized ML workflow orchestration on Kubernetes

### Data & Features
- [[feature-store-patterns]] — centralized feature management, training-serving consistency

### Delivery & Automation
- [[ci-cd-for-ml]] — continuous integration and deployment for ML systems

### Observability & Operations
- [[observability-for-ml-systems]] — instrumentation and monitoring for production ML

---

## Graph Relationships

```
                    ┌─────────────────────┐
                    │  ci-cd-for-ml       │
                    └──────┬──────────────┘
                           │
              triggers     │     validates
         ┌─────────────────┼─────────────────┐
         ▼                 ▼                  ▼
┌─────────────────┐ ┌─────────────┐ ┌──────────────────┐
│ kubeflow-       │ │ mlflow-     │ │ docker-layer-    │
│ pipelines       │ │ model-      │ │ caching          │
│                 │ │ registry    │ │                  │
└────────┬────────┘ └──────┬──────┘ └──────────────────┘
         │                  │
    produces           monitors
         │                  │
         ▼                  ▼
┌─────────────────┐ ┌──────────────────────┐
│ feature-store-  │ │ model-drift-         │
│ patterns        │ │ monitoring           │
└────────┬────────┘ └──────────┬───────────┘
         │                      │
    feeds into              subset of
         │                      │
         ▼                      ▼
         └──────────┬───────────┘
                    ▼
         ┌──────────────────────┐
         │ observability-for-   │
         │ ml-systems           │
         └──────────────────────┘
```

---

## Architecture Notes (Planned)

- `ml-platform-architecture` — end-to-end ML platform design
- `model-serving-patterns` — real-time vs. batch vs. streaming inference
- `multi-model-systems` — ensemble, routing, and cascade architectures
- `ml-security-architecture` — adversarial robustness, model theft, data poisoning

---

## Operational Playbooks (Planned)

- `runbook-model-rollback` — emergency model reversion procedure
- `runbook-drift-investigation` — systematic drift root cause analysis
- `runbook-pipeline-failure` — debugging failed training pipelines
- `runbook-feature-incident` — responding to feature store outages

---

## Debugging Patterns (Planned)

- `debugging-training-serving-skew` — diagnosing feature mismatch between environments
- `debugging-silent-model-failure` — when metrics are fine but outcomes are wrong
- `debugging-pipeline-nondeterminism` — reproducibility failures in distributed training
- `debugging-latency-spikes` — inference performance degradation patterns

---

## Infrastructure Concepts (Planned)

- `gpu-scheduling-strategies` — resource allocation for training and inference
- `model-artifact-storage` — versioned storage patterns (S3, DBFS, GCS)
- `secrets-management-for-ml` — handling API keys, credentials in pipelines
- `cost-optimization-ml-infra` — right-sizing compute for ML workloads

---

## MLOps Workflows (Planned)

- `retraining-trigger-patterns` — when and how to retrain (scheduled, drift-triggered, event-driven)
- `ab-testing-models` — traffic splitting, statistical significance, decision criteria
- `shadow-deployment` — testing new models without user impact
- `champion-challenger-pattern` — structured model comparison in production

---

## Glossary / Terminology (Planned)

- `glossary-mlops` — canonical definitions for MLOps terminology
- `glossary-ml-metrics` — precision, recall, F1, AUC, RMSE with operational context
- `glossary-infrastructure` — containers, orchestration, observability terminology

---

## Integration Points

### AWS Connections
- [[amazon-bedrock]] — managed ML services
- [[aws-s3]] — artifact and data storage
- [[lambda]] — event-driven ML automation
- [[glue]] — data preprocessing at scale

### Databricks Connections
- [[databricks]] — unified analytics platform
- [[delta-lake]] — data layer for ML features and artifacts
- [[databricks-notebooks]] — experimentation environment

### AI/ML Foundations
- [[rag]] — retrieval-augmented generation (RAG as MLOps challenge)
- [[embeddings]] — vector representations in ML systems
- [[model-evaluation]] — evaluation methodology

### Data Engineering Foundations
- [[data-pipeline]] — upstream data flow
- [[etl]] / [[elt]] — data transformation patterns
- [[data-warehouse]] — structured analytical storage

---

## Cross-Cutting Themes

| Theme | Relevant Notes |
|---|---|
| Reproducibility | mlflow-model-registry, kubeflow-pipelines, ci-cd-for-ml |
| Governance | model-drift-monitoring, feature-store-patterns, mlflow-model-registry |
| Observability | observability-for-ml-systems, model-drift-monitoring |
| Automation | ci-cd-for-ml, kubeflow-pipelines |
| Infrastructure | docker-layer-caching, kubeflow-pipelines |
| Data Quality | feature-store-patterns, model-drift-monitoring |

---

## KodeKloud 100 Days of MLOps — Integration Layer

### Program Overview
The KodeKloud 100 Days of MLOps program provides the operational practice layer for
this knowledge system. Tools covered: DVC, MLflow, Feast, Kubernetes, Argo Workflows,
Evidently — real infrastructure, not simulations.

### Four-Layer Knowledge Flow
```
KodeKloud (practice) → Databricks (journal) → Obsidian (evergreen) → GitHub (portfolio)
```

### Process Documentation
- [[mlops-documentation-pipeline]] — end-to-end workflow diagram (Mermaid)
- [[kodekloud-to-evergreen-conversion]] — when daily tasks become durable notes
- [[naming-conventions]] — cross-system naming alignment
- [[github-repo-structure]] — portfolio repo architecture

### Templates
- [[databricks-daily-journal-template]] — structured daily notebook
- [[databricks-weekly-recap-template]] — weekly synthesis notebook

### Anticipated Evergreen Notes from 100 Days
| Week Range | Domain | Expected Notes |
|---|---|---|
| 1-2 | Containers & Environments | docker-layer-caching, container-registries |
| 3-4 | Data Versioning & Tracking | dvc-data-versioning, experiment-tracking |
| 5-6 | Model Management | mlflow-model-registry, model-serving-patterns |
| 7-8 | Feature Engineering | feature-store-patterns, feature-freshness |
| 9-10 | Orchestration | kubeflow-pipelines, argo-workflows |
| 11-12 | Monitoring & Observability | model-drift-monitoring, observability-for-ml-systems |
| 13-14 | CI/CD & Governance | ci-cd-for-ml, ml-governance-framework |
| 15 | Capstone Integration | end-to-end-mlops-architecture |

---

## Learning Sources

- **KodeKloud 100 Days of MLOps**: Primary operational practice layer (DVC, MLflow, Feast, K8s, Argo, Evidently)
- **KodeKloud Fundamentals of MLOps**: Conceptual foundations course
- **KodeKloud MLOps for AIOps**: MLflow + Kubeflow deep dive
- AWS certifications: Cloud Practitioner, AI Practitioner → service-level understanding
- Databricks: Lakehouse architecture, MLflow → platform-specific patterns
- Google MLOps whitepaper: Maturity levels and automation strategies
- Chip Huyen: Designing Machine Learning Systems

---

## Related MOCs

- [[moc-ai-ml]] — foundational ML concepts
- [[moc-aws-cloud]] — AWS infrastructure knowledge
- [[moc-databricks]] — Databricks platform knowledge
- [[moc-data-sql]] — data engineering foundations
- [[moc-projects]] — portfolio project connections
