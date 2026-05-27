---
title: MLflow Model Registry
type: evergreen
domain: mlops
status: seed
visibility: PORTFOLIO_SAFE
rag_ready: true
created: 2026-05-27
last_updated: 2026-05-27
tags:
  - mlops
  - mlflow
  - model-registry
  - reproducibility
  - governance
  - databricks
  - aws
  - quantpath
aliases:
  - model registry
  - MLflow registry
  - model versioning
---

# MLflow Model Registry

**Summary**: A centralized model store that provides versioning, stage transitions, lineage tracking, and governance controls for machine learning models across their lifecycle — from experimentation through production deployment.

**Type**: Evergreen note
**Domain**: MLOps / Model Management
**Status**: Seed
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2026-05-27

---

## Core Concept

The Model Registry is the organizational backbone of production ML. It answers the questions that matter in operational contexts:

- **Which model is in production right now?**
- **Who promoted it, when, and why?**
- **What data and parameters produced this artifact?**
- **Can we roll back safely if this model degrades?**

Without a registry, models exist as orphaned files — unnamed, unversioned, and ungoverned. The registry transforms models from research artifacts into managed organizational assets.

---

## Architectural Role

```
┌─────────────────────────────────────────────────────────────┐
│                    MLflow Ecosystem                          │
├─────────────┬──────────────────┬────────────────────────────┤
│  Tracking   │  Model Registry  │  Model Serving             │
│  Server     │  (this note)     │  (deployment targets)      │
├─────────────┼──────────────────┼────────────────────────────┤
│ - run_id    │ - model name     │ - SageMaker endpoint       │
│ - params    │ - version #      │ - Databricks serving       │
│ - metrics   │ - stage          │ - Lambda / container       │
│ - artifacts │ - lineage        │ - Kubernetes               │
└─────────────┴──────────────────┴────────────────────────────┘
```

The registry sits between experimentation (tracking) and deployment (serving). It is the governance checkpoint.

---

## Key Abstractions

### Registered Model
A named entity that groups all versions of a model trained for a specific task.

### Model Version
An immutable snapshot tied to a specific MLflow run. Each version stores:
- Artifact URI (S3, DBFS, local)
- Run ID (full lineage to parameters, metrics, data)
- Description and tags
- Creation timestamp

### Stage Transitions (Legacy) / Aliases (Current)
- **Legacy stages**: `None → Staging → Production → Archived`
- **Current approach (MLflow 2.x+)**: Named aliases (`champion`, `challenger`) assigned to specific versions
- Aliases are more flexible — multiple deployment targets, A/B testing patterns

### Model Signatures
Input/output schema definitions that enable runtime validation. Critical for catching schema drift before it reaches production.

---

## Why This Matters in Production

1. **Auditability**: Regulators and stakeholders need to know which model made a decision, when it was deployed, and what data trained it.
2. **Rollback capability**: When a model degrades, the registry enables instant reversion to the previous champion.
3. **Collaboration**: Multiple data scientists can propose challenger models without disrupting the production model.
4. **Reproducibility**: Every version links back to the exact run, code, and data snapshot that produced it.
5. **Deployment automation**: CI/CD pipelines trigger on stage transitions or alias reassignments.

---

## Failure Modes and Risks

| Failure Mode | Impact | Mitigation |
|---|---|---|
| No signature enforcement | Silent schema drift in production | Require signatures on all registered models |
| Manual stage transitions | Ungoverned promotions, audit gaps | Automate via webhooks + approval gates |
| Orphaned versions | Storage bloat, confusion | Retention policies, auto-archive after N days |
| Single registry for all envs | Dev models pollute prod namespace | Namespace isolation or separate registries per env |
| Missing run lineage | Cannot reproduce or debug model | Enforce run_id linkage at registration time |

---

## Governance Considerations

- **Access control**: Who can promote to production? Role-based permissions on stage transitions.
- **Approval workflows**: Webhooks can trigger Slack notifications, Jira tickets, or human-in-the-loop gates before promotion.
- **Model cards**: Attach documentation (intended use, limitations, fairness metrics) to each registered model.
- **Retention policies**: Define how long archived models are retained for audit purposes.
- **Lineage requirements**: Enforce that every registered version has a linked experiment run with logged parameters, metrics, and dataset references.

---

## AWS Relevance

- **SageMaker Model Registry**: AWS's native equivalent; integrates with SageMaker Pipelines
- **MLflow on SageMaker**: Managed MLflow available as a SageMaker feature
- **S3 as artifact store**: Model artifacts stored in S3 with versioning enabled
- **IAM integration**: Control registry access via IAM policies and roles
- **Lambda triggers**: Stage transitions can invoke Lambda for deployment automation

## Databricks Relevance

- **Unity Catalog integration**: Models registered in Unity Catalog gain workspace-level governance
- **Databricks Model Serving**: Direct deployment from registry to real-time endpoints
- **Webhooks**: Native webhook support for stage-transition automation
- **Feature Store lineage**: Models track which Feature Store tables they consumed
- **Workspace ACLs**: Fine-grained permissions on model CRUD operations

---

## Integration Patterns

### CI/CD Integration
```yaml
# Pseudocode: GitHub Actions trigger on model promotion
on:
  mlflow_webhook:
    event: model_version_transitioned
    stage: Production

jobs:
  deploy:
    steps:
      - validate-model-signature
      - run-integration-tests
      - deploy-to-endpoint
      - notify-stakeholders
```

### A/B Testing with Aliases
```python
# Register challenger alongside champion
client.set_registered_model_alias("fraud_detector", "challenger", version=12)
# Traffic splitting handled at serving layer
# Promote when metrics confirm improvement
client.set_registered_model_alias("fraud_detector", "champion", version=12)
```

---

## Portfolio / Project Integration Opportunities

- **QuantPath ML models**: Register rate-regime classifiers or affordability models as versioned artifacts
- **Bedrock RAG pipeline**: Track embedding model versions used for knowledge base updates
- **CFPB dashboard**: Version any anomaly detection or trend models used in analysis
- **Databricks workflows**: Integrate Databricks model serving with registry-triggered deployment

---

## Related Notes

- [[ci-cd-for-ml]] — deployment automation triggered by registry events
- [[model-drift-monitoring]] — monitoring models post-deployment
- [[observability-for-ml-systems]] — tracking model behavior in production
- [[feature-store-patterns]] — lineage between features and registered models
- [[kubeflow-pipelines]] — pipeline orchestration that feeds the registry
- [[moc-mlops]] — MLOps knowledge map

---

## Sources and Further Reading

- MLflow Documentation: Model Registry
- Databricks: Unity Catalog for ML
- AWS: SageMaker Model Registry
- Google: ML Metadata (MLMD) — alternative lineage approach
