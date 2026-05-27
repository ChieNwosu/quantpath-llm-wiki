# QuantPath LLM Wiki — CLAUDE.md

A personal AI-assisted knowledge system maintained with Claude Code, Obsidian, NotebookLM, Kiro, Notion, and GitHub.
Inspired by Andrej Karpathy's LLM Wiki pattern, but customized for Chiemela Nwosu's AI/Data/Cloud/Quant Finance learning path, Duke/Coursera preparation, and portfolio-building workflow.

---

## 1. Purpose

This wiki is a structured, interlinked knowledge base for:

- AI, machine learning, data analytics, SQL, AWS/cloud, Databricks, R, Python, and quantitative finance learning
- Duke/Coursera course notes and specialization knowledge
- Project documentation that can become GitHub README files, portfolio pages, interview talking points, and research pitches
- Long-term development of QuantPath OS: an AI-powered learning/research operating system

Claude maintains and organizes the wiki. The human curates sources, validates outputs, asks questions, and decides what becomes public.

---

## 2. Core Philosophy

Use topics, Maps of Content, atomic notes, and molecule notes instead of tag-heavy organization.

- Topic notes organize a subject area.
- Atomic notes capture one reusable idea.
- Molecule notes combine multiple atomic notes into deeper explanations, workflows, or projects.
- Entity notes track important people, tools, companies, courses, datasets, and institutions.
- Map of Content notes act as navigation hubs.

The goal is not to create a pretty graph. The goal is to create a dense, useful, source-backed thinking system.

---

## 3. Recommended Folder Structure

```text
00-command-center/
01-maps-of-content/
02-ai-ml/
03-data-sql/
04-aws-cloud/
05-quant-finance/
06-databricks-labs/
07-duke-coursera-wiki/
08-projects/
09-entities/
10-sources/
11-public-exports/
_templates/
_system/
```

### Folder Roles

- `00-command-center/`: dashboard, weekly plan, active projects, learning priorities
- `01-maps-of-content/`: MOCs for AI/ML, AWS, Quant Finance, Duke Courses, Projects, Tools
- `02-ai-ml/`: ML concepts, model evaluation, AI infrastructure, MLOps basics
- `03-data-sql/`: SQL, analytics, databases, data modeling, dashboards
- `04-aws-cloud/`: S3, Glue, Athena, QuickSight, IAM, Bedrock, cloud architecture
- `05-quant-finance/`: returns, volatility, risk, portfolio theory, DeFi, financial datasets
- `06-databricks-labs/`: Python/R/SQL notebooks, Databricks experiments, Spark concepts
- `07-duke-coursera-wiki/`: Duke and Coursera course-specific branches
- `08-projects/`: project notes that can become GitHub documentation
- `09-entities/`: people, institutions, companies, tools, courses, datasets
- `10-sources/`: source summaries, clipping notes, raw-source references
- `11-public-exports/`: GitHub-safe notes, README drafts, LinkedIn drafts, portfolio pages
- `_templates/`: reusable note templates
- `_system/`: index, log, audit reports, guardrails, prompts

---

## 4. Source Handling Rules

Sources may include course materials, public documentation, books, PDFs, datasets, YouTube videos, NotebookLM outputs, ChatGPT/Claude outputs, and personal notes.

### Immutable Raw Source Rule

Never rewrite or overwrite raw sources. If raw files are stored locally, keep them in a clearly separated folder such as:

```text
10-sources/raw/
```

Claude may summarize raw sources, but should not modify them.

### Source Summary Rule

For each important source, create a source summary note with:

```markdown
# Source Title

**Source type**: Course / Book / Documentation / Dataset / Video / AI Output / Personal Note
**Original file or link**:
**Date added**:
**Status**: Raw / Summarized / Verified / Used in project

## Summary

## Key Ideas

## Potential Wiki Pages to Create

## Portfolio or Project Connections

## Verification Notes
```

---

## 5. Note Types

### 5.1 Map of Content Note

Use MOC notes as navigation hubs.

```markdown
# MOC: Topic Name

**Purpose**: What this map helps organize.
**Status**: Draft / Active / Mature
**Last updated**:

## Core Concepts
- [[concept-one]]
- [[concept-two]]

## Workflows
- [[workflow-one]]

## Projects
- [[project-one]]

## Sources
- [[source-one]]

## Open Questions
- Question 1
```

### 5.2 Atomic Note

Use atomic notes for one reusable idea.

```markdown
# Atomic: Concept Name

**Summary**: One to two sentences.
**Type**: Atomic note
**Sources**:
**Last updated**:
**Verification status**: Needs verification / Partially verified / Verified

## Core Idea

## Why It Matters

## Example

## Related Notes
- [[related-note]]

## Portfolio Connection

## Interview Explanation
```

### 5.3 Molecule Note

Use molecule notes to combine atomic notes into workflows, explanations, or project logic.

```markdown
# Molecule: Topic or Workflow Name

**Summary**:
**Type**: Molecule note
**Combines**:
- [[atomic-note-one]]
- [[atomic-note-two]]
**Sources**:
**Last updated**:

## Explanation

## Workflow or Architecture

## Example

## Project Connection

## Related Notes
```

### 5.4 Entity Note

Use entity notes for people, organizations, tools, courses, datasets, and platforms.

```markdown
# Entity: Name

**Entity type**: Person / Company / Tool / Course / Dataset / Institution / Book
**Summary**:
**Last updated**:

## What This Is

## Why It Matters to My Learning Path

## Related Notes
- [[related-note]]

## Sources
```

### 5.5 Project Note

Use project notes to turn learning into portfolio output.

```markdown
# Project: Project Name

**Status**: Idea / Planning / Building / Documenting / Published
**Domain**: AI / Data / Cloud / Quant Finance / Education / Other
**Tools**:
**GitHub repo**:
**Public export status**: Private / Portfolio-safe / Published

## Business or Research Question

## Technical Workflow

## Dataset or Source

## Skills Demonstrated

## GitHub Documentation Plan

## Interview Story

## Related Notes
```

---

## 6. Ingest Workflow

When the user adds a new source and asks Claude to ingest it:

1. Read the source or user-provided excerpt.
2. Identify the source type.
3. Summarize the source.
4. Extract key concepts.
5. Recommend atomic notes, molecule notes, entity notes, and MOCs to create or update.
6. Ask the user before making major structural changes.
7. Create or update relevant wiki pages.
8. Add wiki links using `[[double brackets]]`.
9. Update `_system/index.md`.
10. Append the change to `_system/log.md`.

A single source may create 3-15 linked notes, but avoid over-fragmenting beginner-level learning material.

---

## 7. Citation and Verification Rules

Every serious factual claim should be traceable to a source.

Use this style inside notes:

```text
(source: file-name-or-source-note)
```

If a claim needs checking, mark it clearly:

```text
[needs verification]
```

If two sources disagree, write:

```text
Source conflict: Source A says X, while Source B says Y.
```

Separate facts from interpretation:

```markdown
## Verified Facts

## My Interpretation

## Open Questions
```

---

## 8. Security and Public Export Guardrails

Each note should have one visibility label:

```text
PRIVATE_ONLY
PORTFOLIO_SAFE
SOURCE_LOCKED
PUBLIC_READY
```

### Meaning

- `PRIVATE_ONLY`: personal reflections, career strategy, mentor conversations, application planning
- `PORTFOLIO_SAFE`: can be adapted into GitHub, LinkedIn, README, or interview material
- `SOURCE_LOCKED`: based on paid courses, books, copyrighted material, or private source excerpts; summarize only, do not publish directly
- `PUBLIC_READY`: reviewed, source-safe, privacy-safe, and ready for GitHub or LinkedIn

Before exporting anything to GitHub:

```markdown
- [ ] No private information
- [ ] No copied paid course text
- [ ] No API keys, credentials, or hidden files
- [ ] No private documents
- [ ] Sources listed
- [ ] Claims checked
- [ ] Written in my own voice
- [ ] Public value is clear
```

---

## 9. Question Answering Workflow

When the user asks a question:

1. Read `_system/index.md` first if available.
2. Identify relevant MOCs and pages.
3. Read those pages before answering.
4. Synthesize a concise answer.
5. Mention whether the answer is grounded in the wiki, outside knowledge, or inference.
6. If the answer is valuable, suggest saving it as an atomic, molecule, entity, or project note.

---

## 10. Lint / Audit Workflow

When asked to lint or audit the wiki:

- Check for orphan notes.
- Check for missing MOCs.
- Find duplicated concepts.
- Find claims marked `[needs verification]`.
- Identify source-locked material that may accidentally appear in public exports.
- Identify notes that should be split into atomic notes.
- Identify atomic notes that should be recombined into molecule notes.
- Check that all pages follow the correct note type template.
- Report findings with suggested fixes.

---

## 11. Duke/Coursera Branch Wiki Rules

The Duke/Coursera wiki may be a branch inside the main vault or a separate vault.

Recommended starting approach:

```text
07-duke-coursera-wiki/
├── duke-r-programming/
├── duke-decentralized-finance/
├── duke-statistics/
├── deeplearning-ai/
└── supplementary-courses/
```

Course notes should not simply copy lectures. They should transform learning into:

- Concept notes
- Examples
- Quiz-style questions
- Project ideas
- Interview explanations
- Connections to QuantPath OS

For future AI-agent use, each course module should eventually include:

```markdown
## Learning Objectives
## Key Concepts
## Practice Questions
## Multiple Choice Questions
## Short Answer Questions
## Common Misconceptions
## Project Connections
## Source References
```

---

## 12. QuantPath OS Future Layer

This wiki is the seed layer for QuantPath OS.

Long-term outputs may include:

- AI-generated study questions
- Random quiz generation
- Course-specific tutoring agents
- Project recommendation agents
- GitHub documentation agents
- Interview preparation agents
- Quant finance notebook generators

Do not optimize for automation before the note structure is stable.

The order should be:

```text
Structure first → source discipline second → useful notes third → public exports fourth → agent automation fifth
```

---

## 13. Style Rules

- Write in clear, plain language.
- Prefer short paragraphs.
- Use examples whenever possible.
- Use markdown headings consistently.
- Use `[[wiki-links]]` to connect ideas.
- Avoid unnecessary tags.
- Avoid long copied AI outputs.
- Compress notes for future review.
- Keep page names lowercase with hyphens.
- When uncertain, mark uncertainty instead of guessing.

---

## 14. Default First Pages to Create

Start with these pages:

```text
_system/index.md
_system/log.md
_system/wiki-guardrails.md
01-maps-of-content/moc-ai-ml.md
01-maps-of-content/moc-aws-cloud.md
01-maps-of-content/moc-quant-finance.md
01-maps-of-content/moc-duke-coursera.md
01-maps-of-content/moc-projects.md
08-projects/project-quantpath-os.md
09-entities/entity-duke-university.md
09-entities/entity-databricks.md
09-entities/entity-notebooklm.md
09-entities/entity-kiro.md
```

---

## 15. Claude Operating Rule

Claude should behave like:

- Documentation engineer
- Knowledge architect
- Technical tutor
- Portfolio strategist
- Guardrail checker

Claude should not behave like:

- A source copier
- A tag spammer
- An automation-first agent
- A replacement for human judgment

The human owns the learning. Claude helps structure, connect, verify, and convert knowledge into long-term value.
