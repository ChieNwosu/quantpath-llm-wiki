---
title: "KodeKloud-to-Evergreen Conversion System"
type: process
domain: mlops
status: active
visibility: PORTFOLIO_SAFE
rag_ready: true
created: 2026-05-27
last_updated: 2026-05-27
tags:
  - mlops
  - kodekloud
  - evergreen
  - knowledge-management
  - quantpath
aliases:
  - conversion system
  - note promotion
  - daily-to-evergreen
  - task conversion framework
---

# KodeKloud-to-Evergreen Conversion System

**Purpose**: A decision framework for determining when and how a KodeKloud daily task should be promoted into a durable knowledge artifact — and which type of artifact it should become.

---

## Core Principle

**Not every daily task deserves an evergreen note.**

Most days produce *procedural memory* (I did X, Y, Z). Only some days produce *conceptual insight* (I now understand WHY systems work this way). The conversion system separates signal from noise.

---

## The Promotion Decision Matrix

```
┌──────────────────────────────────────────────────────────────────────┐
│                    Promotion Decision Tree                             │
├──────────────────────────────────────────────────────────────────────┤
│                                                                        │
│  After completing a KodeKloud daily task, ask:                        │
│                                                                        │
│  Q1: Did I learn a CONCEPT or just execute a PROCEDURE?               │
│  ├── Procedure only → Daily log only (GitHub)                         │
│  └── Concept → Continue to Q2                                         │
│                                                                        │
│  Q2: Is this concept ALREADY captured in an existing evergreen note?  │
│  ├── Yes → UPDATE existing note (add new insight, example, or link)   │
│  └── No → Continue to Q3                                              │
│                                                                        │
│  Q3: Is this concept DURABLE (true regardless of tool version)?       │
│  ├── No → Tool-specific reference note (GitHub /tools/)               │
│  └── Yes → Continue to Q4                                             │
│                                                                        │
│  Q4: Is this concept about STRUCTURE or about FIXING?                 │
│  ├── Structure → Architecture note or Evergreen note                  │
│  └── Fixing → Debugging playbook                                      │
│                                                                        │
│  Q5 (for structure): Is this a SYSTEMS RELATIONSHIP or a CONCEPT?     │
│  ├── Systems relationship → Architecture note                         │
│  └── Standalone concept → Evergreen note                              │
│                                                                        │
└──────────────────────────────────────────────────────────────────────┘
```

---

## Artifact Types and Criteria

### 1. Daily Log Only

**Destination**: GitHub `daily-logs/` + Databricks notebook (remains as-is)
**Criteria**: The task was execution-focused with no transferable insight beyond "I know how to run this command."

**Examples**:
- Installing a tool for the first time
- Following a guided lab with no surprises
- Repeating a pattern already captured elsewhere
- Configuration that is project-specific, not conceptual

**Template action**: Fill daily journal in Databricks, export to GitHub log. Done.

---

### 2. Evergreen Note

**Destination**: Obsidian `07-mlops/evergreen/` + GitHub `evergreen-exports/`
**Criteria**: ALL of the following must be true:

- [ ] Concept is durable (true in 3 years regardless of tool version)
- [ ] Concept is atomic (one idea, fully self-contained)
- [ ] Concept has production relevance (matters in real systems)
- [ ] Concept has failure modes (can go wrong in interesting ways)
- [ ] Concept connects to other vault knowledge (≥2 wikilinks)
- [ ] You can explain it without referencing the specific lab

**Examples**:
- "Model registries solve the versioning problem by..." (from Day 14: MLflow lab)
- "Training-serving skew occurs because..." (from Day 28: Feature Store lab)
- "Container layer caching reduces build time by..." (from Day 4: Docker lab)

**Promotion process**:
1. Identify the concept from the daily journal's Reflection section
2. Check if the concept already exists in the vault → update if yes
3. Draft the note using vault note structure (frontmatter, sections, failure modes)
4. Add wikilinks to/from related notes
5. Update `moc-mlops.md` with the new entry
6. Mark the daily journal's `evergreen_flag: true`

---

### 3. Architecture Note

**Destination**: Obsidian `07-mlops/architecture/` + GitHub `architecture/`
**Criteria**: The insight is about HOW SYSTEMS RELATE, not a single concept.

- [ ] Describes interaction between ≥2 components
- [ ] Involves design decisions with tradeoffs
- [ ] Could be drawn as a diagram
- [ ] Answers "why is it built this way?" not "what is it?"

**Examples**:
- "MLflow + Kubernetes model serving architecture" (spans registry + deployment)
- "Feature Store read patterns in training vs. serving" (spans offline + online store)
- "CI/CD pipeline stages for ML" (spans testing + validation + deployment)

**Promotion process**:
1. Multiple daily tasks reveal a cross-cutting architectural pattern
2. Draft an architecture note with diagrams (Mermaid preferred)
3. Link to all related evergreen notes
4. Typically created during weekly recap (when patterns emerge across days)

---

### 4. Debugging Playbook

**Destination**: Obsidian `07-mlops/debugging/` + GitHub `playbooks/`
**Criteria**: You encountered a failure that taught you something about system behavior.

- [ ] The failure was non-obvious (not a typo or missing import)
- [ ] The root cause reveals system architecture or assumptions
- [ ] Other people would encounter this same failure
- [ ] The resolution teaches a diagnostic technique

**Examples**:
- "Docker build hangs at pip install" → reveals layer caching invalidation
- "MLflow experiment not logging metrics" → reveals tracking URI misconfiguration
- "Kubeflow pipeline step OOMKilled" → reveals resource request patterns
- "Feature values differ between training and serving" → reveals skew patterns

**Playbook structure**:
1. **Symptom**: What you observed
2. **Expected behavior**: What should have happened
3. **Root cause**: Why it failed (system-level explanation)
4. **Diagnostic steps**: How to confirm the cause
5. **Resolution**: How to fix it
6. **Prevention**: How to avoid it in the future
7. **Related concepts**: Links to evergreen notes

---

### 5. GitHub Portfolio Artifact (standalone)

**Destination**: GitHub repo only (not necessarily in Obsidian)
**Criteria**: The artifact demonstrates engineering capability to an external reviewer.

- [ ] Shows working code or configuration
- [ ] Demonstrates problem-solving process
- [ ] Could be discussed in an interview
- [ ] Has visual appeal (diagrams, clean formatting)

**Examples**:
- A complete Docker Compose stack for local MLflow
- A CI/CD pipeline YAML with model validation gates
- A monitoring dashboard configuration
- A capstone project design document

---

## Conversion Timing

| When | Action |
|---|---|
| During daily task | Flag potential promotions in journal (set `evergreen_flag`, `portfolio_flag`) |
| End of day | Quick 2-minute assessment: "Was today conceptual or procedural?" |
| Weekly recap | Review all flagged days, batch-create evergreen notes |
| Monthly review | Identify architecture notes that span multiple weeks |
| End of program | Synthesize capstone from accumulated architecture notes |

---

## Volume Expectations

Over 100 days, expect approximately:

| Artifact Type | Expected Count | Ratio |
|---|---|---|
| Daily logs | 100 | 100% of days |
| Evergreen notes | 15-25 | ~20% of days produce new concepts |
| Architecture notes | 5-10 | ~1 per 2 weeks |
| Debugging playbooks | 10-15 | ~1 per week |
| Tool reference updates | 30-40 | ~every 2-3 days |
| Portfolio artifacts | 8-12 | ~1 per week |

**Total vault growth**: ~50-80 new or updated notes over 100 days.

---

## Quality Gate: When NOT to Promote

Do NOT create an evergreen note when:
- You're just paraphrasing documentation (no original insight)
- The concept is too tool-specific to survive a version change
- You can't articulate failure modes (understanding is shallow)
- An existing note already covers it (update instead)
- The note would be < 200 words of substance (too thin to be atomic)

---

## Workflow Integration

```
KodeKloud Task
     │
     ▼
Databricks Daily Journal
     │
     ├── [End of day] Flag: evergreen? architecture? playbook?
     │
     ▼
Weekly Recap
     │
     ├── Review all flags
     ├── Batch-promote flagged items
     ├── Create/update vault notes
     │
     ▼
Monthly Review
     │
     ├── Identify cross-week architecture patterns
     ├── Validate RAG-readiness of new notes
     ├── Update MOC
     │
     ▼
GitHub Push (weekly)
     │
     ├── Daily logs (always)
     ├── Evergreen exports (when promoted)
     ├── Architecture notes (when created)
     └── Playbooks (when created)
```

---

## Related Notes

- [[vault-practices]] — note quality standards and RAG-readiness
- [[naming-conventions]] — cross-system naming alignment
- [[github-repo-structure]] — where artifacts land in the portfolio repo
- [[databricks-daily-journal-template]] — source template with promotion flags
- [[databricks-weekly-recap-template]] — weekly review drives batch promotion
- [[moc-mlops]] — MLOps knowledge map (updated on promotion)
