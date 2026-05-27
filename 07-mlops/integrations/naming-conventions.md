---
title: "Naming Conventions — Cross-System Alignment"
type: process
domain: mlops
status: active
visibility: PORTFOLIO_SAFE
rag_ready: true
created: 2026-05-27
last_updated: 2026-05-27
tags:
  - mlops
  - naming
  - conventions
  - kodekloud
  - databricks
  - quantpath
aliases:
  - naming alignment
  - file naming
  - cross-system naming
---

# Naming Conventions — Cross-System Alignment

**Purpose**: Establish consistent naming patterns across all four layers of the MLOps learning infrastructure — ensuring discoverability, traceability, and alignment between KodeKloud tasks, Databricks notebooks, Obsidian vault notes, and GitHub portfolio artifacts.

---

## The Four-Layer Naming Problem

Each system has different constraints:

| System | Constraints | Separator | Case |
|---|---|---|---|
| KodeKloud | Fixed by platform (not controllable) | N/A | N/A |
| Databricks | No special chars, Workspace paths | `_` (underscore) | `snake_case` |
| Obsidian | Filename = note title, URL-safe preferred | `-` (hyphen) | `kebab-case` |
| GitHub | URL-safe, readable in browser | `_` for logs, `-` for concepts | `snake_case` / `kebab-case` |

---

## Canonical Naming Scheme

### Rule 1: Day Number is the Universal Key

Every daily artifact begins with the day number formatted as **three-digit zero-padded integer**.

```
Day 1   → 001
Day 14  → 014
Day 100 → 100
```

This enables:
- Natural sort order across all systems
- Cross-referencing by number regardless of platform
- Chronological browsing without metadata lookup

### Rule 2: Topic Slug is Shared Across Systems

Derive a **canonical topic slug** from the KodeKloud task. This slug appears (with platform-appropriate formatting) in all four systems.

**Derivation rules**:
1. Identify the core concept (not the task action)
2. Use 2-4 words maximum
3. Prefer established MLOps terminology
4. Remove articles (a, the, an)
5. Prefer nouns over verbs

**Example derivations**:

| KodeKloud Task Title | Canonical Topic Slug |
|---|---|
| "Set up MLflow Tracking Server" | `mlflow_tracking_setup` |
| "Build a Multi-Stage Docker Image" | `docker_multi_stage_builds` |
| "Configure DVC Remote Storage" | `dvc_remote_storage` |
| "Deploy Model with Kubernetes" | `kubernetes_model_deployment` |
| "Monitor Data Drift with Evidently" | `evidently_data_drift` |
| "Create Feature Pipeline with Feast" | `feast_feature_pipeline` |

---

## Per-System Naming Patterns

### Databricks Notebooks

**Pattern**: `day_NNN_topic_slug`

```
day_001_environment_setup
day_014_mlflow_model_registry
day_028_feast_feature_pipeline
day_045_kubeflow_pipeline_basics
day_067_evidently_data_drift
day_100_capstone_integration
```

**Weekly recaps**: `week_NN_recap_theme`
```
week_01_recap_containers
week_02_recap_version_control
week_08_recap_monitoring
```

**Rules**:
- All lowercase
- Underscore separators
- No special characters
- No spaces
- Maximum 50 characters

### Obsidian Vault Notes

**Pattern (evergreen)**: `concept-name.md` (no day number — concepts are timeless)

```
mlflow-model-registry.md
docker-layer-caching.md
feature-store-patterns.md
dvc-data-versioning.md
evidently-drift-detection.md
```

**Pattern (daily reference)**: stored in Databricks, NOT duplicated in vault. The vault contains only evergreen concepts, not daily logs.

**Rules**:
- Kebab-case (hyphens)
- Concept-centered naming (noun phrases)
- No day numbers (evergreen notes transcend chronology)
- No tool version numbers

### GitHub Daily Logs

**Pattern**: `day_NNN_topic_slug.md`

```
daily-logs/week-01/day_001_environment_setup.md
daily-logs/week-02/day_014_mlflow_model_registry.md
daily-logs/week-04/day_028_feast_feature_pipeline.md
```

**Rules**:
- Snake_case for filenames (matches Databricks)
- Organized in `week-NN/` subdirectories
- Three-digit day number always present

### GitHub Architecture Notes

**Pattern**: `concept-name.md` (matches Obsidian style)

```
architecture/feature-store-design.md
architecture/model-serving-patterns.md
playbooks/debugging-mlflow-tracking.md
```

**Rules**:
- Kebab-case (hyphens)
- Concept-centered
- Matches Obsidian naming for exported notes

---

## Cross-Reference Table

| Day | KodeKloud Task | Databricks Notebook | Obsidian Note | GitHub Log |
|---|---|---|---|---|
| 014 | MLflow Model Registry Lab | `day_014_mlflow_model_registry` | `mlflow-model-registry.md` | `daily-logs/week-02/day_014_mlflow_model_registry.md` |
| 028 | Feast Feature Pipeline | `day_028_feast_feature_pipeline` | `feature-store-patterns.md` | `daily-logs/week-04/day_028_feast_feature_pipeline.md` |
| 045 | Kubeflow Pipeline Basics | `day_045_kubeflow_pipeline_basics` | `kubeflow-pipelines.md` | `daily-logs/week-07/day_045_kubeflow_pipeline_basics.md` |
| 067 | Evidently Data Drift | `day_067_evidently_data_drift` | `model-drift-monitoring.md` | `daily-logs/week-10/day_067_evidently_data_drift.md` |

**Key insight**: Databricks notebooks and GitHub daily logs share EXACT naming (snake_case + day number). Obsidian notes use CONCEPT names (kebab-case, no day number) because multiple days may feed into a single evergreen note.

---

## Tag Alignment

Tags should also be consistent across systems:

| Concept | Obsidian Tag | GitHub Topic/Label | Databricks Folder |
|---|---|---|---|
| Experiment tracking | `#mlflow` | `mlflow` | `/mlops-journal/experiment-tracking/` |
| Containers | `#docker` | `docker` | `/mlops-journal/containers/` |
| Orchestration | `#kubeflow` | `kubeflow` | `/mlops-journal/orchestration/` |
| Monitoring | `#observability` | `monitoring` | `/mlops-journal/monitoring/` |
| Features | `#feature-engineering` | `feature-store` | `/mlops-journal/features/` |
| Data versioning | `#dvc` | `dvc` | `/mlops-journal/data-versioning/` |
| Governance | `#governance` | `governance` | `/mlops-journal/governance/` |

---

## Naming Decision Flowchart

```
Is this a daily task output?
├── YES → day_NNN_topic_slug (snake_case, with day number)
│         Used in: Databricks notebook name, GitHub daily log filename
│
└── NO → Is this a durable concept?
         ├── YES → concept-name (kebab-case, no day number)
         │         Used in: Obsidian vault, GitHub architecture/evergreen-exports
         │
         └── NO → Is this a weekly synthesis?
                  ├── YES → week_NN_recap_theme (snake_case)
                  │         Used in: Databricks, GitHub weekly-recaps
                  │
                  └── Is this a playbook?
                       └── YES → debugging-symptom-description (kebab-case)
                                 Used in: Obsidian vault, GitHub playbooks
```

---

## Anti-Patterns

| Don't | Why | Do Instead |
|---|---|---|
| `Day14-MLflow.md` | Inconsistent case, no padding | `day_014_mlflow_model_registry.md` |
| `mlflow_model_registry.md` (in Obsidian) | Vault uses kebab-case | `mlflow-model-registry.md` |
| `day-014-mlflow` (in GitHub logs) | Logs use snake_case | `day_014_mlflow_model_registry.md` |
| `MLOps Day 14 Notes` (Databricks) | Spaces, capitals, vague | `day_014_mlflow_model_registry` |
| `notes-from-kodekloud.md` | Non-specific, undiscoverable | Use concept-based naming |
| `week1.md` | No padding, no theme | `week_01_recap_containers.md` |

---

## Related Notes

- [[github-repo-structure]] — full portfolio repo layout
- [[databricks-daily-journal-template]] — notebook naming in context
- [[vault-practices]] — Obsidian naming standards
- [[kodekloud-to-evergreen-conversion]] — when daily tasks become evergreen
- [[moc-mlops]] — MLOps knowledge map
