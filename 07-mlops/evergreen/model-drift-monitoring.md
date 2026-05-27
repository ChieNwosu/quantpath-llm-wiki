---
title: Model Drift Monitoring
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
  - model-drift
  - monitoring
  - governance
  - aws
  - databricks
  - quantpath
aliases:
  - drift detection
  - concept drift
  - data drift
  - model degradation
  - model staleness
---

# Model Drift Monitoring

**Summary**: Model drift monitoring is the practice of continuously measuring whether the statistical properties of model inputs, outputs, or real-world outcomes have shifted relative to training-time baselines — detecting when a deployed model is no longer reliable before business impact occurs.

**Type**: Evergreen note
**Domain**: MLOps / Monitoring / Governance
**Status**: Seed
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2026-05-27

---

## Core Concept

Every deployed ML model embodies assumptions about the world at training time. The world changes. Drift monitoring detects when the gap between training assumptions and production reality becomes operationally significant.

There are three fundamental drift types:

### 1. Data Drift (Covariate Shift)
The distribution of input features changes, but the relationship between features and target remains the same.

**Example**: A mortgage affordability model trained on 2019-2022 data sees dramatically different rate distributions in 2024. Input features shift, even if the underlying economic relationships hold.

### 2. Concept Drift
The relationship between inputs and the correct output changes.

**Example**: "Affordable" mortgage payment thresholds shift as wage growth and inflation change consumer behavior. Same inputs should now produce different outputs.

### 3. Prediction Drift (Output Drift)
The distribution of model predictions changes, regardless of whether inputs or concepts shifted.

**Example**: A fraud model starts flagging 15% of transactions instead of 2% — even if each individual prediction is still "correct," the operational impact is dramatic.

---

## Detection Framework

```
┌────────────────────────────────────────────────────────────────┐
│                    Drift Detection Stack                         │
├────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Reference Window          Production Window                     │
│  (training data dist.)     (recent predictions)                  │
│  ┌──────────────────┐     ┌──────────────────┐                 │
│  │ P(X) at train    │     │ P(X) in prod     │                 │
│  │ P(Y|X) at train  │     │ P(Y|X) in prod   │                 │
│  │ P(Ŷ) at train    │     │ P(Ŷ) in prod     │                 │
│  └────────┬─────────┘     └────────┬─────────┘                 │
│           │                         │                            │
│           └──────────┬──────────────┘                            │
│                      ▼                                           │
│  ┌──────────────────────────────────────────────┐               │
│  │  Statistical Tests                            │               │
│  │  - KS test (continuous features)              │               │
│  │  - Chi-squared (categorical features)         │               │
│  │  - PSI (Population Stability Index)           │               │
│  │  - Jensen-Shannon divergence                  │               │
│  │  - Wasserstein distance                       │               │
│  └──────────────────────┬───────────────────────┘               │
│                          ▼                                       │
│  ┌──────────────────────────────────────────────┐               │
│  │  Alert / Action                               │               │
│  │  - Notify team                                │               │
│  │  - Trigger retraining                         │               │
│  │  - Activate fallback model                    │               │
│  │  - Human-in-the-loop escalation               │               │
│  └──────────────────────────────────────────────┘               │
│                                                                  │
└────────────────────────────────────────────────────────────────┘
```

---

## Statistical Methods

### Population Stability Index (PSI)
- Most common in financial services
- Measures shift between two distributions
- `PSI < 0.1`: No significant shift
- `PSI 0.1-0.25`: Moderate shift — investigate
- `PSI > 0.25`: Significant shift — action required

### Kolmogorov-Smirnov Test
- Non-parametric test for continuous distributions
- Measures maximum distance between CDFs
- Good for detecting distribution shape changes

### Jensen-Shannon Divergence
- Symmetric version of KL divergence
- Bounded [0, 1] — easier to interpret and threshold
- Works for both continuous and discrete distributions

### Page-Hinkley Test
- Sequential change detection
- Detects gradual drift (not just sudden shifts)
- Low memory footprint — suitable for streaming

---

## Monitoring Architecture Patterns

### Pattern 1: Batch Monitoring
- Scheduled comparison of recent predictions vs. reference
- Suitable for models with daily/weekly prediction cycles
- Lower infrastructure cost, higher detection latency

### Pattern 2: Streaming Monitoring
- Real-time statistical tracking on every prediction
- Suitable for high-throughput, low-latency models
- Uses windowed statistics and sequential tests

### Pattern 3: Ground Truth Feedback Loop
- Compare predictions to actual outcomes when labels arrive
- Gold standard but often delayed (labels may take days/weeks)
- Essential for concept drift detection

### Pattern 4: Shadow Scoring
- New model scores alongside production model
- Detects drift by comparing agreement rates over time
- No user impact during evaluation period

---

## Why This Matters in Production

1. **Silent degradation prevention**: Models degrade gradually — without monitoring, nobody notices until business metrics collapse.
2. **Proactive retraining signals**: Drift alerts trigger retraining before performance drops below acceptable thresholds.
3. **Root cause diagnosis**: Feature-level drift monitoring identifies *which* inputs are changing, guiding data engineering responses.
4. **Regulatory compliance**: Financial and healthcare models require documented evidence that models remain valid.
5. **Trust maintenance**: Stakeholders lose confidence in ML systems that produce unexplained behavior changes.

---

## Failure Modes and Risks

| Failure Mode | Impact | Mitigation |
|---|---|---|
| Alert fatigue | Real drift ignored among false positives | Tiered alerting, statistical significance thresholds |
| Delayed ground truth | Concept drift undetectable for weeks | Proxy metrics, prediction distribution monitoring |
| Reference window staleness | Baseline becomes irrelevant over time | Sliding reference windows, periodic baseline refresh |
| Feature-level blind spots | Drift in unmeasured features goes undetected | Monitor all model inputs, including derived features |
| Threshold miscalibration | Too sensitive (noise) or too lenient (miss real drift) | A/B test thresholds, adapt based on historical drift patterns |
| Survivorship bias | Only monitoring successful predictions | Monitor rejected/filtered inputs separately |

---

## Governance Considerations

- **Mandatory monitoring**: Production models without drift monitoring should not be approved for deployment.
- **Escalation protocols**: Define who is notified at each drift severity level and required response times.
- **Regulatory documentation**: Maintain evidence that models are monitored and that drift events are investigated.
- **Model validity periods**: Define maximum time between validations — even without detected drift.
- **Bias drift**: Monitor protected-attribute distributions in predictions to detect emerging fairness violations.
- **Incident retrospectives**: Every significant drift event produces a documented root cause analysis.

---

## AWS Relevance

- **SageMaker Model Monitor**: Managed drift detection with baseline constraints
- **CloudWatch**: Custom metrics for model performance and drift statistics
- **Kinesis**: Streaming prediction ingestion for real-time monitoring
- **Lambda**: Trigger retraining or alerts on drift threshold breach
- **QuickSight**: Drift visualization dashboards for stakeholders

## Databricks Relevance

- **Lakehouse Monitoring**: Table-level data quality and drift monitoring
- **MLflow + Evidently**: Drift metrics logged alongside model metrics
- **Delta Live Tables expectations**: Data quality gates that catch upstream drift
- **Inference Tables**: Automatic logging of predictions for post-hoc drift analysis
- **Alerts**: Databricks SQL alerts on drift metric thresholds

---

## Tool Landscape

| Tool | Type | Strengths |
|---|---|---|
| Evidently AI | OSS library + dashboard | Feature-rich, easy integration |
| WhyLabs | Managed platform | Real-time, profile-based monitoring |
| NannyML | OSS library | Performance estimation without ground truth |
| SageMaker Monitor | AWS managed | Integrated with SageMaker ecosystem |
| Arize AI | Managed platform | Production ML observability |
| Fiddler AI | Managed platform | Explainability + drift combined |

---

## Portfolio / Project Integration Opportunities

- **Mortgage rate regime detection**: Monitor when current rate behavior drifts from historical patterns
- **CFPB complaint models**: Detect when complaint patterns shift (new product categories, changing sentiment)
- **Bedrock RAG**: Monitor query distribution drift — are users asking different questions over time?
- **Affordability models**: Rate environment changes constitute natural concept drift — perfect case study

---

## Related Notes

- [[observability-for-ml-systems]] — drift monitoring as subset of ML observability
- [[feature-store-patterns]] — feature drift as leading indicator
- [[mlflow-model-registry]] — drift triggers model version transitions
- [[ci-cd-for-ml]] — drift-triggered retraining pipelines
- [[moc-mlops]] — MLOps knowledge map

---

## Sources and Further Reading

- Google: Monitoring ML Models in Production
- Evidently AI: ML Monitoring Course
- NannyML: Estimating Performance without Ground Truth
- AWS: SageMaker Model Monitor Documentation
- Sculley et al.: "Hidden Technical Debt in Machine Learning Systems"
