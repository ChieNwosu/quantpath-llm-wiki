---
title: "GitHub Repo Structure — 100 Days of MLOps Portfolio"
type: architecture
domain: mlops
status: active
visibility: PORTFOLIO_SAFE
rag_ready: true
created: 2026-05-27
last_updated: 2026-05-27
tags:
  - mlops
  - github
  - portfolio
  - documentation
  - kodekloud
  - quantpath
aliases:
  - 100 days repo structure
  - MLOps portfolio repo
  - GitHub MLOps layout
---

# GitHub Repo Structure — 100 Days of MLOps Portfolio

**Purpose**: Define the file and folder architecture for the public-facing GitHub repository that documents the KodeKloud 100 Days of MLOps journey as a production-minded engineering portfolio artifact.

**Repo name**: `quantpath-100-days-mlops` (proposed)

---

## Repository Layout

```
quantpath-100-days-mlops/
│
├── README.md                           ← Project overview, philosophy, navigation
├── CHANGELOG.md                        ← Weekly progress log (auto-updated)
├── LICENSE                             ← MIT or CC-BY-4.0 for documentation
├── .gitignore
│
├── daily-logs/                         ← One markdown file per completed day
│   ├── week-01/
│   │   ├── day_001_environment_setup.md
│   │   ├── day_002_docker_fundamentals.md
│   │   ├── day_003_dockerfile_ml.md
│   │   ├── day_004_docker_layer_caching.md
│   │   ├── day_005_docker_compose_ml.md
│   │   ├── day_006_multi_stage_builds.md
│   │   └── day_007_container_registries.md
│   ├── week-02/
│   │   └── ...
│   └── week-15/
│       └── ...
│
├── weekly-recaps/                      ← Weekly synthesis documents
│   ├── week_01_containers_and_environments.md
│   ├── week_02_version_control_for_ml.md
│   └── ...
│
├── notebooks/                          ← Exported Databricks notebooks (.py or .html)
│   ├── daily/
│   │   ├── day_001_environment_setup.py
│   │   └── ...
│   ├── weekly/
│   │   ├── week_01_recap.py
│   │   └── ...
│   └── capstone/
│       └── ...
│
├── architecture/                       ← System design and architecture notes
│   ├── ml-pipeline-architecture.md
│   ├── feature-store-design.md
│   ├── model-serving-patterns.md
│   ├── monitoring-stack-design.md
│   └── end-to-end-mlops-architecture.md
│
├── diagrams/                           ← Visual artifacts (Mermaid source + rendered)
│   ├── mermaid/
│   │   ├── mlops-documentation-pipeline.mmd
│   │   ├── ci-cd-ml-flow.mmd
│   │   └── feature-store-architecture.mmd
│   ├── rendered/
│   │   ├── mlops-documentation-pipeline.png
│   │   └── ...
│   └── README.md                       ← Index of all diagrams with descriptions
│
├── playbooks/                          ← Operational runbooks and debugging guides
│   ├── debugging-docker-build-failures.md
│   ├── debugging-mlflow-tracking-issues.md
│   ├── debugging-k8s-pod-scheduling.md
│   ├── rollback-model-deployment.md
│   └── investigate-model-drift.md
│
├── evergreen-exports/                  ← Selected Obsidian notes exported for public use
│   ├── README.md                       ← Explains relationship to full vault
│   ├── mlflow-model-registry.md
│   ├── docker-layer-caching.md
│   ├── feature-store-patterns.md
│   ├── ci-cd-for-ml.md
│   ├── kubeflow-pipelines.md
│   ├── model-drift-monitoring.md
│   └── observability-for-ml-systems.md
│
├── capstone/                           ← End-of-program capstone documentation
│   ├── README.md                       ← Capstone overview and architecture
│   ├── design-document.md
│   ├── implementation-notes.md
│   ├── evaluation-results.md
│   └── lessons-learned.md
│
├── tools/                              ← Tool-specific reference notes
│   ├── dvc-reference.md
│   ├── mlflow-reference.md
│   ├── feast-reference.md
│   ├── evidently-reference.md
│   ├── argo-workflows-reference.md
│   └── kubernetes-ml-reference.md
│
└── .github/
    ├── ISSUE_TEMPLATE/
    │   └── daily-log-checklist.md      ← Template for tracking daily completion
    └── workflows/
        └── validate-markdown.yml       ← CI: lint markdown, check links
```

---

## Folder Purposes

### `daily-logs/`
**One file per day. Organized by week.**

Content per file:
- Day number, date, topic
- Objective (what the task required)
- Tools/concepts practiced
- Key commands (with WHY context)
- What broke and how it was fixed
- Production relevance
- Evergreen note connections
- Portfolio value assessment

**Naming**: `day_NNN_snake_case_topic.md`
**Grouping**: `week-NN/` subdirectories (7 days each)

### `weekly-recaps/`
**Synthesis over listing. Principles over procedures.**

Content per file:
- Days completed with status
- Concepts consolidated
- Architecture lessons
- Reusable MLOps principles
- Failure pattern analysis
- Next-week focus

**Naming**: `week_NN_theme_description.md`

### `notebooks/`
**Exported Databricks notebooks for reproducibility evidence.**

- `daily/` — individual day journals (exported as `.py` or `.html`)
- `weekly/` — recap notebooks
- `capstone/` — final project notebooks

Export format: `.py` preferred (version-control friendly), `.html` for rich display

### `architecture/`
**Design-level documentation. Not tutorials.**

These are the notes that demonstrate systems thinking:
- How components relate
- Why certain architectures are chosen
- Tradeoffs and alternatives considered
- Scaling implications

### `diagrams/`
**Visual system documentation.**

- `mermaid/` — source files (`.mmd`) for version control
- `rendered/` — PNG exports for GitHub display
- Mermaid preferred because GitHub renders it natively in markdown

### `playbooks/`
**Operational knowledge distilled from debugging experiences.**

Each playbook answers: "When X happens, do Y because Z."

Structure per playbook:
1. Symptom (what you observe)
2. Possible causes (ranked by likelihood)
3. Diagnostic steps
4. Resolution
5. Prevention

### `evergreen-exports/`
**Selected Obsidian vault notes published for portfolio visibility.**

Rules:
- Only `visibility: PORTFOLIO_SAFE` notes are exported
- Remove Obsidian-specific syntax (wikilinks → standard links)
- Add "Part of the QuantPath MLOps Knowledge System" header
- Keep YAML frontmatter for metadata

### `capstone/`
**End-of-program synthesis project.**

Demonstrates:
- End-to-end MLOps pipeline design
- Integration of tools learned across 100 days
- Production-readiness thinking
- Architecture decision records

### `tools/`
**Quick-reference notes for each major tool in the stack.**

Not tutorials — operational reference:
- Installation/setup patterns
- Key commands with context
- Common failure modes
- Integration points with other tools
- AWS/Databricks equivalents

---

## File Conventions

### Markdown Standards
- GitHub Flavored Markdown (GFM)
- YAML frontmatter on all files (for future tooling)
- Mermaid diagrams inline where supported
- Tables for structured comparisons
- Code blocks with language tags and WHY comments

### Frontmatter Template (Daily Log)
```yaml
---
day: 14
date: 2026-06-15
topic: MLflow Model Registry
domain: experiment-tracking
tools: [mlflow, python, docker]
kodekloud_module: Model Management
status: complete
portfolio_flag: true
evergreen_flag: true
---
```

### Frontmatter Template (Architecture Note)
```yaml
---
title: Feature Store Design Patterns
type: architecture
domain: feature-engineering
created: 2026-06-20
status: active
related_days: [23, 24, 25, 41]
---
```

---

## Branching Strategy

```
main (protected)
  └── week-NN (weekly batch PRs)
        └── day-NNN-topic (individual day work if needed)
```

- **Weekly PRs**: Batch daily logs + recap into one PR per week
- **Architecture PRs**: Separate branch for design documents
- **Capstone PR**: Dedicated branch for final project

---

## CI/CD (Optional Future)

```yaml
# .github/workflows/validate-markdown.yml
name: Validate Documentation
on: [push, pull_request]
jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: DavidAnson/markdownlint-cli2-action@v16
      - name: Check internal links
        run: npx markdown-link-check **/*.md
```

---

## Growth Pattern

| Week | Expected Additions |
|---|---|
| 1-2 | Daily logs, first tool references, initial diagrams |
| 3-4 | First architecture notes, first playbooks |
| 5-8 | Evergreen exports begin, architecture depth increases |
| 9-12 | Playbook library grows, cross-referencing matures |
| 13-15 | Capstone development, final architecture synthesis |

---

## Portfolio Presentation

This repo is designed to be reviewed by:
- **Technical recruiters**: See consistent engineering practice over 100 days
- **Hiring managers**: Assess systems thinking via architecture notes
- **ML engineers**: Evaluate operational depth via playbooks and failure analysis
- **Non-technical stakeholders**: Navigate via README and weekly recaps

---

## Related Notes

- [[naming-conventions]] — cross-system naming alignment
- [[kodekloud-to-evergreen-conversion]] — promotion decision framework
- [[databricks-daily-journal-template]] — source notebook template
- [[vault-practices]] — Obsidian vault standards
- [[moc-mlops]] — MLOps knowledge map
