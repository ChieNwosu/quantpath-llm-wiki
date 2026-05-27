---
title: CI/CD for ML
type: evergreen
domain: mlops
status: seed
visibility: PORTFOLIO_SAFE
rag_ready: true
created: 2026-05-27
last_updated: 2026-05-27
tags:
  - mlops
  - ci-cd
  - testing
  - reproducibility
  - governance
  - aws
  - databricks
  - quantpath
aliases:
  - ML CI/CD
  - continuous integration for machine learning
  - ML deployment pipeline
  - model delivery pipeline
---

# CI/CD for ML

**Summary**: CI/CD for ML extends traditional software delivery practices to handle the unique challenges of machine learning systems — where code, data, model artifacts, and configuration all change independently and must be validated together before production deployment.

**Type**: Evergreen note
**Domain**: MLOps / Delivery / Automation
**Status**: Seed
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2026-05-27

---

## Core Concept

Traditional CI/CD validates code changes. ML CI/CD must validate three coupled dimensions:

```
┌───────────────────────────────────────────────┐
│          ML CI/CD: Three Dimensions           │
├───────────────┬───────────────┬───────────────┤
│    Code       │    Data       │    Model      │
├───────────────┼───────────────┼───────────────┤
│ Unit tests    │ Schema valid. │ Metric gates  │
│ Lint/format   │ Distribution  │ Signature     │
│ Integration   │ Freshness     │ Bias/fairness │
│ Dependency    │ Completeness  │ Latency       │
│ Security scan │ Lineage       │ Size/memory   │
└───────────────┴───────────────┴───────────────┘
```

A code change might not affect model quality. A data change might break a model without any code change. A retrained model might degrade despite identical code and data pipelines. Each dimension requires its own validation strategy.

---

## ML CI/CD Maturity Levels

### Level 0: Manual Process
- Jupyter notebooks → manual deployment
- No version control on experiments
- "It worked on my machine" as the only validation

### Level 1: ML Pipeline Automation
- Automated training pipeline
- Experiment tracking (MLflow)
- Manual deployment trigger

### Level 2: CI/CD Pipeline Automation
- Automated training + automated deployment
- Model validation gates
- A/B testing infrastructure
- Monitoring-triggered retraining

### Level 3: Full MLOps
- Feature store integration
- Automated retraining on data drift
- Canary deployments with automatic rollback
- Full lineage and governance

---

## Pipeline Architecture

```
┌─────────┐    ┌─────────┐    ┌──────────┐    ┌──────────┐    ┌─────────┐
│  Code   │───→│  Build  │───→│  Train   │───→│ Validate │───→│ Deploy  │
│  Push   │    │  & Test │    │  & Log   │    │  & Gate  │    │ & Serve │
└─────────┘    └─────────┘    └──────────┘    └──────────┘    └─────────┘
     │              │               │               │               │
     │         ┌────┴────┐    ┌────┴────┐    ┌────┴────┐    ┌────┴────┐
     │         │- Lint   │    │- MLflow │    │- Metric │    │- Canary │
     │         │- Unit   │    │- Params │    │  thresholds│  │- Shadow │
     │         │- Docker │    │- Data   │    │- Bias   │    │- A/B    │
     │         │  build  │    │  snapshot│    │  checks │    │- Rollbk │
     │         └─────────┘    └─────────┘    └─────────┘    └─────────┘
     │
  ┌──┴──────────────────────────────────────────────────────────────┐
  │  Triggers: code push, data update, schedule, drift alert,       │
  │            model registry event, manual approval                 │
  └─────────────────────────────────────────────────────────────────┘
```

---

## Validation Gates

### Code Quality Gates
- Linting and formatting (black, ruff, pylint)
- Unit tests for feature engineering logic
- Integration tests for pipeline components
- Dependency vulnerability scanning
- Docker image builds successfully

### Data Quality Gates
- Schema validation (Great Expectations, Pandera)
- Distribution checks (statistical tests vs. reference)
- Completeness thresholds (null rate, row count)
- Freshness checks (data age within acceptable window)
- Referential integrity (foreign keys resolve)

### Model Quality Gates
- Performance metric thresholds (accuracy, F1, RMSE vs. baseline)
- Regression testing (performance on held-out golden datasets)
- Bias and fairness metrics (demographic parity, equalized odds)
- Latency constraints (p99 inference time within SLA)
- Model size and memory footprint limits
- Input signature validation

---

## Why This Matters in Production

1. **Confidence in deployment**: Automated gates catch regressions before they reach users.
2. **Speed of iteration**: Teams can deploy more frequently because validation is automated.
3. **Reproducibility**: Every deployment is traceable to a specific code version, data snapshot, and training run.
4. **Risk reduction**: Canary deployments and automatic rollbacks limit blast radius.
5. **Regulatory compliance**: Automated documentation of what was tested, when, and by whom.

---

## Failure Modes and Risks

| Failure Mode | Impact | Mitigation |
|---|---|---|
| Testing on stale data | Model validated against unrepresentative data | Date-bounded test datasets, freshness checks |
| Metric gaming | Model overfits to validation set over time | Rotate golden datasets, multiple evaluation dimensions |
| Slow pipelines | Teams bypass CI to deploy faster | Docker layer caching, parallelized stages, incremental tests |
| Flaky tests | False failures erode trust in CI | Deterministic seeds, tolerance bands, retry policies |
| Missing rollback path | Degraded model stays in production | Automated rollback triggers, preserved previous artifacts |
| Config drift | Pipeline works differently across environments | Environment-as-code, config validation in CI |

---

## Governance Considerations

- **Approval gates**: Human-in-the-loop before production deployment for high-risk models
- **Audit logs**: Every pipeline run produces immutable records of inputs, outputs, and decisions
- **Separation of duties**: Model developers cannot self-approve production promotions
- **Compliance documentation**: Auto-generated model cards and validation reports
- **Change management**: All pipeline changes require PR review with ML-aware reviewers
- **Incident linkage**: Failed deployments automatically create incident tickets

---

## AWS Relevance

- **CodePipeline / CodeBuild**: Native CI/CD with ML-specific buildspecs
- **SageMaker Pipelines**: Managed ML pipeline orchestration with built-in model evaluation
- **Step Functions**: Complex orchestration for multi-stage ML workflows
- **ECR**: Container registry for ML training and serving images
- **CloudWatch**: Pipeline monitoring and alerting
- **S3**: Artifact storage for models, data snapshots, and test results

## Databricks Relevance

- **Databricks Workflows**: Orchestration for training, validation, and deployment jobs
- **MLflow**: Experiment tracking and model registry integrated into CI
- **Delta Live Tables**: Data quality expectations as pipeline gates
- **Bundle CLI**: Infrastructure-as-code for Databricks ML resources
- **Model Serving**: Deployment target triggered by CI/CD completion

---

## Tool Landscape

| Category | Tools |
|---|---|
| Orchestration | GitHub Actions, GitLab CI, Jenkins, Argo Workflows |
| ML Pipelines | Kubeflow, SageMaker Pipelines, Databricks Workflows |
| Data Validation | Great Expectations, Pandera, Deequ |
| Model Validation | MLflow, custom metric gates, Evidently |
| Deployment | ArgoCD, Seldon, SageMaker, Databricks Serving |
| Monitoring | Evidently, WhyLabs, custom dashboards |

---

## Portfolio / Project Integration Opportunities

- **QuantPath pipeline**: Automated validation when rate data updates trigger reanalysis
- **Bedrock RAG CI**: Validate embedding quality and retrieval accuracy on each knowledge base update
- **Databricks notebooks → jobs**: Convert exploratory notebooks into validated, scheduled pipelines
- **GitHub Actions**: Build CI/CD for any ML component in the QuantPath portfolio

---

## Related Notes

- [[docker-layer-caching]] — build acceleration for ML containers
- [[kubeflow-pipelines]] — pipeline orchestration layer
- [[mlflow-model-registry]] — deployment triggered by registry events
- [[model-drift-monitoring]] — post-deployment validation
- [[feature-store-patterns]] — feature validation in CI
- [[observability-for-ml-systems]] — production monitoring post-deploy
- [[moc-mlops]] — MLOps knowledge map

---

## Sources and Further Reading

- Google: MLOps Continuous Delivery and Automation (CD4ML)
- Martin Fowler: Continuous Delivery for Machine Learning
- AWS: MLOps Workload Orchestrator
- Databricks: MLOps Stacks
