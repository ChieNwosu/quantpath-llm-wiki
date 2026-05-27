---
title: Observability for ML Systems
type: evergreen
domain: mlops
status: seed
visibility: PORTFOLIO_SAFE
rag_ready: true
created: 2026-05-27
last_updated: 2026-05-27
tags:
  - mlops
  - observability
  - monitoring
  - ai-engineering
  - governance
  - aws
  - databricks
  - quantpath
aliases:
  - ML observability
  - model observability
  - production ML monitoring
  - inference monitoring
---

# Observability for ML Systems

**Summary**: ML observability extends traditional software observability (metrics, logs, traces) with ML-specific signals — prediction distributions, feature health, model performance, and explanation stability — providing the instrumentation needed to understand *why* an ML system behaves the way it does in production, not just *that* it is running.

**Type**: Evergreen note
**Domain**: MLOps / Observability / Production Systems
**Status**: Seed
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2026-05-27

---

## Core Concept

Traditional software observability answers: "Is it running? Is it fast? Is it correct?"

ML observability adds: "Is the model still trustworthy? Are predictions still meaningful? Has the world changed in ways that invalidate our model's assumptions?"

The distinction matters because ML systems can be:
- **Operationally healthy** (low latency, no errors, high throughput)
- **Intellectually degraded** (predictions are statistically worthless)

An inference endpoint returning 200 OK with 3ms latency can simultaneously be producing garbage predictions. Traditional monitoring won't catch this. ML observability will.

---

## The Observability Stack for ML

```
┌────────────────────────────────────────────────────────────────────────┐
│                    ML Observability Layers                               │
├────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│  Layer 4: Business Metrics                                               │
│  ┌────────────────────────────────────────────────────────────────┐    │
│  │  Revenue impact, conversion rates, user satisfaction, churn     │    │
│  └────────────────────────────────────────────────────────────────┘    │
│                                                                          │
│  Layer 3: Model Performance                                              │
│  ┌────────────────────────────────────────────────────────────────┐    │
│  │  Accuracy, precision, recall, RMSE (when ground truth arrives)  │    │
│  └────────────────────────────────────────────────────────────────┘    │
│                                                                          │
│  Layer 2: Prediction & Feature Health                                    │
│  ┌────────────────────────────────────────────────────────────────┐    │
│  │  Prediction distribution, feature drift, data quality, freshness│    │
│  └────────────────────────────────────────────────────────────────┘    │
│                                                                          │
│  Layer 1: Infrastructure / Operational                                   │
│  ┌────────────────────────────────────────────────────────────────┐    │
│  │  Latency, throughput, errors, CPU/GPU, memory, disk, network    │    │
│  └────────────────────────────────────────────────────────────────┘    │
│                                                                          │
└────────────────────────────────────────────────────────────────────────┘
```

Each layer provides progressively deeper insight, but with increasing detection latency. Infrastructure metrics are instant; model performance metrics may be delayed by days or weeks (label delay problem).

---

## Key Observability Signals

### Infrastructure Signals
- Request latency (p50, p95, p99)
- Throughput (requests/second)
- Error rates (HTTP 5xx, timeout, OOM)
- GPU utilization and memory
- Container health and restart counts

### Feature Health Signals
- Feature completeness (missing value rates)
- Feature distribution stability (PSI, KS distance vs. baseline)
- Feature freshness (time since last update)
- Schema compliance (type mismatches, out-of-range values)

### Prediction Signals
- Prediction distribution (mean, variance, percentiles over time)
- Confidence score distribution (calibration drift)
- Prediction volume patterns (anomalous request spikes)
- Class balance in outputs (unexpected skew)

### Model Performance Signals (delayed)
- Accuracy / F1 / RMSE vs. baseline (when labels arrive)
- Performance stratified by segment (cohort analysis)
- Explanation stability (SHAP value consistency)
- Fairness metrics across protected groups

---

## The Three Pillars Applied to ML

### Metrics
Quantitative time-series measurements:
- Prediction latency percentiles
- Feature drift statistics per feature
- Model accuracy over sliding windows
- Business KPI correlation with model outputs

### Logs
Structured event records:
- Individual prediction requests + responses
- Feature values at prediction time
- Model version serving the request
- Preprocessing pipeline execution details

### Traces
End-to-end request flow:
- Client request → preprocessing → feature lookup → inference → postprocessing → response
- Per-step latency attribution
- Cross-service dependency mapping (feature store → model → application)

---

## Why This Matters in Production

1. **Root cause diagnosis**: When metrics drop, observability data identifies *which* component failed and *why*.
2. **Early warning system**: Feature drift and prediction distribution shifts are leading indicators of performance degradation.
3. **Debugging at scale**: Individual prediction-level logging enables investigation of specific failure cases.
4. **Accountability**: Complete audit trail of what the model saw, computed, and returned for any given prediction.
5. **Continuous improvement**: Performance analytics reveal which segments or scenarios need model improvement.
6. **Trust building**: Stakeholders can verify model behavior without requiring ML expertise.

---

## Failure Modes and Risks

| Failure Mode | Impact | Mitigation |
|---|---|---|
| Monitoring gaps at ML layer | Model degrades silently despite healthy infra | Implement all four observability layers |
| Log volume explosion | Unsustainable storage costs, slow queries | Sampling strategies, tiered retention |
| Metric overload | Alert fatigue, missed real issues | Hierarchical alerting, correlation analysis |
| Missing baselines | No reference for "normal" behavior | Establish baselines during validation, before deployment |
| Observability overhead | Monitoring slows inference | Async logging, sampling, lightweight instrumentation |
| Incomplete traces | Cannot attribute latency to specific stages | Propagate trace context through all pipeline stages |

---

## Governance Considerations

- **Prediction logging compliance**: PII in predictions may require anonymization or restricted access.
- **Retention policies**: Define how long prediction logs are stored (regulatory requirements vary).
- **Access tiering**: Operational teams see infrastructure metrics; governance teams access fairness dashboards.
- **Incident response SLAs**: Define response time requirements for each alert severity level.
- **Audit readiness**: Regulators may request "why did the model produce this output for this customer?"
- **Bias monitoring**: Continuous fairness metrics across protected characteristics with escalation protocols.

---

## AWS Relevance

- **CloudWatch**: Infrastructure metrics, custom ML metrics, dashboards
- **SageMaker Model Monitor**: Managed data quality, model quality, bias, and explainability monitoring
- **X-Ray**: Distributed tracing for inference pipelines
- **Kinesis + Firehose**: Streaming prediction logs to S3 or OpenSearch
- **OpenSearch**: Log aggregation and search for prediction debugging
- **QuickSight**: Business-metric dashboards correlated with model performance

## Databricks Relevance

- **Inference Tables**: Automatic request/response logging for model serving endpoints
- **Lakehouse Monitoring**: Table-level monitoring for feature stores and prediction tables
- **MLflow**: Metric tracking and comparison across model versions
- **SQL Alerts**: Threshold-based alerting on drift and performance metrics
- **Unity Catalog Lineage**: Trace data flow from source through features to predictions

---

## Implementation Patterns

### Pattern 1: Inference Table Architecture
```
Prediction Request → Model Endpoint → Response
                         │
                         ├──→ Inference Table (Delta Lake)
                         │      - request_id
                         │      - timestamp
                         │      - model_version
                         │      - features (JSON)
                         │      - prediction
                         │      - confidence
                         │      - latency_ms
                         │
                         └──→ Metrics Pipeline
                                - Aggregate statistics
                                - Drift detection
                                - Alert generation
```

### Pattern 2: Multi-Signal Correlation
When model performance drops:
1. Check infrastructure (is it even running correctly?)
2. Check feature health (did input data change?)
3. Check prediction distribution (is output abnormal?)
4. Check upstream data (did source systems change?)
5. Check model version (was a new model deployed?)

---

## Tool Landscape

| Category | Tools |
|---|---|
| Infrastructure | Prometheus, Grafana, Datadog, CloudWatch |
| ML-Specific | Arize, WhyLabs, Evidently, Fiddler |
| Logging | OpenSearch, Loki, CloudWatch Logs |
| Tracing | Jaeger, X-Ray, OpenTelemetry |
| Dashboards | Grafana, QuickSight, Tableau |
| Alerting | PagerDuty, OpsGenie, custom Lambda |

---

## Portfolio / Project Integration Opportunities

- **QuantPath model monitoring**: Track rate-regime model predictions and feature health over time
- **Bedrock RAG observability**: Monitor retrieval quality, response latency, and query patterns
- **CFPB dashboard**: Observability for any analytical models powering the dashboard
- **Learning lab**: Build a minimal observability stack (Prometheus + Grafana + custom ML metrics) as portfolio project

---

## Related Notes

- [[model-drift-monitoring]] — drift detection as subset of observability
- [[feature-store-patterns]] — feature health monitoring
- [[mlflow-model-registry]] — model version tracking in production
- [[ci-cd-for-ml]] — pre-deployment validation complementing post-deployment monitoring
- [[kubeflow-pipelines]] — pipeline execution observability
- [[moc-mlops]] — MLOps knowledge map

---

## Sources and Further Reading

- Google SRE Book: Monitoring Distributed Systems
- Arize AI: ML Observability Fundamentals
- OpenTelemetry: Instrumentation for ML Services
- Sculley et al.: "Hidden Technical Debt in ML Systems"
- AWS: SageMaker Model Monitor Documentation
