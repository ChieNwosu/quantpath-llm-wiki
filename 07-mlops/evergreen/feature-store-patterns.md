---
title: Feature Store Patterns
type: evergreen
domain: mlops
status: seed
visibility: PORTFOLIO_SAFE
rag_ready: true
created: 2026-05-27
last_updated: 2026-05-27
tags:
  - mlops
  - feature-engineering
  - feature-store
  - data-governance
  - databricks
  - aws
  - quantpath
aliases:
  - feature store
  - feature management
  - feature platform
  - online/offline store
---

# Feature Store Patterns

**Summary**: A feature store is a centralized system for defining, computing, storing, and serving ML features — solving the training-serving skew problem and enabling feature reuse, governance, and point-in-time correctness across teams and models.

**Type**: Evergreen note
**Domain**: MLOps / Feature Engineering / Data Infrastructure
**Status**: Seed
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2026-05-27

---

## Core Concept

The feature store exists because ML systems have a fundamental duality problem:

- **Training**: needs historical features computed at past points in time (batch, offline)
- **Serving**: needs current features computed in real-time (online, low-latency)

Without a feature store, teams duplicate feature logic across training scripts and serving code. This duplication causes **training-serving skew** — the silent killer of ML system reliability.

A feature store provides:
1. **Single source of truth** for feature definitions
2. **Dual materialization** — same logic produces both offline (training) and online (serving) features
3. **Point-in-time correctness** — prevents data leakage during training
4. **Discovery and reuse** — teams find and share features instead of rebuilding them
5. **Governance** — ownership, lineage, access control, and documentation

---

## Architecture

```
┌──────────────────────────────────────────────────────────────────┐
│                     Feature Store Architecture                     │
├──────────────────────────────────────────────────────────────────┤
│                                                                    │
│  Data Sources          Feature Store              Consumers        │
│  ┌──────────┐         ┌──────────────┐          ┌──────────┐    │
│  │ Raw Data │──┐      │  Feature     │     ┌───→│ Training │    │
│  │ (S3/DB)  │  │      │  Definitions │     │    │ Pipeline │    │
│  └──────────┘  │      │  (code+meta) │     │    └──────────┘    │
│                 ├─────→├──────────────┤─────┤                     │
│  ┌──────────┐  │      │ Offline Store│     │    ┌──────────┐    │
│  │ Streaming│──┘      │ (S3/Delta)   │     └───→│ Serving  │    │
│  │ (Kafka)  │         ├──────────────┤     ┌───→│ Endpoint │    │
│  └──────────┘         │ Online Store │─────┘    └──────────┘    │
│                        │ (Redis/DDB)  │                           │
│                        └──────────────┘                           │
└──────────────────────────────────────────────────────────────────┘
```

---

## Key Patterns

### 1. Offline Store (Batch Features)
- Stores historical feature values for training data generation
- Typically backed by data lake (S3, Delta Lake, Parquet)
- Enables point-in-time joins — "what were this entity's features at time T?"
- Optimized for throughput, not latency

### 2. Online Store (Real-Time Features)
- Stores latest feature values for inference-time lookup
- Backed by low-latency stores (Redis, DynamoDB, Cassandra)
- Key-value access pattern: entity_id → feature_vector
- Optimized for p99 latency (< 10ms)

### 3. Feature Definitions as Code
```python
# Example: Feast feature definition
@feature_view(
    entities=[customer],
    ttl=timedelta(days=1),
    online=True,
    source=customer_transactions_source,
)
def customer_features(inputs):
    return inputs.select(
        "avg_transaction_30d",
        "transaction_count_7d",
        "days_since_last_purchase",
    )
```

### 4. Point-in-Time Joins
The most critical correctness guarantee:
- When generating training data, features must reflect values **as they existed at prediction time**
- Prevents future data from leaking into historical training examples
- Requires event-time semantics, not processing-time

### 5. Feature Freshness Tiers
| Tier | Latency | Example | Compute |
|---|---|---|---|
| Batch | Hours | Customer lifetime value | Scheduled Spark job |
| Near-real-time | Minutes | Session click count | Streaming aggregation |
| Real-time | Milliseconds | Current cart total | Request-time computation |

---

## Why This Matters in Production

1. **Training-serving skew elimination**: Same feature definitions serve both paths — no divergence.
2. **Feature reuse across teams**: One team's features become organizational assets, not siloed scripts.
3. **Data leakage prevention**: Point-in-time semantics prevent subtle but catastrophic training errors.
4. **Faster model development**: Data scientists discover existing features instead of recomputing from raw data.
5. **Operational efficiency**: Centralized computation avoids redundant processing of the same features.

---

## Failure Modes and Risks

| Failure Mode | Impact | Mitigation |
|---|---|---|
| Training-serving skew | Model performance degrades silently in production | Enforce single feature definition for both paths |
| Data leakage via future features | Inflated training metrics, production disappointment | Point-in-time join enforcement, feature lag validation |
| Online store staleness | Predictions based on outdated features | Freshness SLAs, monitoring, alerting on lag |
| Feature definition sprawl | Redundant features, unclear ownership | Governance layer, naming conventions, deprecation policies |
| Schema drift | Feature type changes break downstream models | Schema registry, backward compatibility checks |
| Cold-start entities | New users have no features | Default/fallback feature values, cold-start strategies |

---

## Governance Considerations

- **Ownership**: Every feature group must have a designated owner team responsible for quality and freshness.
- **Access control**: Sensitive features (PII, financial) require role-based access with audit logging.
- **Data lineage**: Feature → source data → raw event chain must be traceable for regulatory compliance.
- **Documentation**: Each feature requires a description, business logic, known limitations, and valid value ranges.
- **Deprecation policy**: Features cannot be removed without migration plan for all consuming models.
- **Quality contracts**: Define SLAs for freshness, completeness, and accuracy per feature tier.

---

## AWS Relevance

- **SageMaker Feature Store**: Native AWS offering with online/offline stores
- **DynamoDB**: Common online store backend for low-latency feature serving
- **S3 + Glue**: Offline store with schema catalog for feature discovery
- **Kinesis**: Streaming source for near-real-time feature computation
- **Athena**: Ad-hoc querying of offline feature history for debugging

## Databricks Relevance

- **Databricks Feature Store**: Integrated with Unity Catalog for governance
- **Delta Lake**: Offline store with time-travel for point-in-time correctness
- **Feature Serving endpoints**: Low-latency online serving from Databricks
- **MLflow lineage**: Automatic tracking of which features trained which model version
- **Unity Catalog**: Centralized governance for feature tables, models, and data assets

---

## Implementation Landscape

| Tool | Strengths | Tradeoffs |
|---|---|---|
| Feast (OSS) | Flexible, cloud-agnostic, active community | Operational overhead, self-managed |
| Databricks Feature Store | Unity Catalog integration, managed | Vendor lock-in |
| SageMaker Feature Store | AWS-native, managed | AWS-only, less flexible |
| Tecton | Enterprise-grade, real-time focus | Cost, complexity |
| Hopsworks | Open-source, full-featured | Self-hosted complexity |

---

## Portfolio / Project Integration Opportunities

- **Mortgage rate features**: Store rate-regime indicators, rolling volatility, affordability metrics as reusable features
- **CFPB analysis**: Consumer complaint features for anomaly detection or trend models
- **Bedrock RAG**: Document-level features (freshness, relevance scores) for retrieval optimization
- **Databricks workflows**: Feature Store as central layer between raw FRED data and analytical models

---

## Related Notes

- [[mlflow-model-registry]] — models track which features they consumed
- [[model-drift-monitoring]] — feature drift as leading indicator of model drift
- [[ci-cd-for-ml]] — feature validation in CI pipelines
- [[observability-for-ml-systems]] — feature freshness and quality monitoring
- [[data-pipeline]] — upstream data feeding feature computation
- [[moc-mlops]] — MLOps knowledge map

---

## Sources and Further Reading

- Feast Documentation
- Databricks: Feature Store Best Practices
- Google: Towards ML Engineering (Feature Stores chapter)
- Uber: Michelangelo Feature Store
- Tecton: What is a Feature Store?
