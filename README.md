# QuantPath LLM Wiki

> A personal knowledge operating system for AI/data/cloud engineering, quantitative finance, and applied machine learning.

**Status**: Active learning system — work in progress
**Visibility**: Private (under review for selective public release)
**Maintained by**: Chiemela Nwosu

---

## Purpose

This repository is the QuantPath LLM Wiki: a structured, interlinked Markdown knowledge base maintained in [Obsidian](https://obsidian.md) and version-controlled with Git.

It is inspired by Andrej Karpathy's LLM Wiki pattern — the idea that a well-structured personal knowledge graph compounds over time into a durable thinking and reference system.

The vault supports:
- Evergreen technical concept notes
- Applied project documentation
- AWS/cloud certification study
- Quantitative finance and financial modeling
- Databricks and Spark learning journals
- MLOps and AI systems documentation
- Duke/Coursera and IBM certificate learning
- Future RAG (Retrieval-Augmented Generation) deployment via Amazon Bedrock
- AI-assisted note ingestion via NotebookLM and Kiro

---

## What the Vault Contains

| Folder | Contents |
|---|---|
| `00-command-center/` | Dashboard, roadmap, active priorities |
| `01-maps-of-content/` | MOC navigation hubs by domain |
| `02-ai-ml/` | AI/ML concept notes (RAG, embeddings, classification, etc.) |
| `03-data-sql/` | SQL, data modeling, pipelines, ETL/ELT |
| `04-aws-cloud/` | AWS services, cloud architecture, certification notes |
| `05-quant-finance/` | Quantitative finance, financial modeling, mortgage analytics |
| `06-databricks-labs/` | Databricks, Spark, Delta Lake, lab notes |
| `07-duke-coursera-wiki/` | Duke/Coursera and IBM certificate course notes |
| `08-projects/` | Portfolio project documentation |
| `09-entities/` | People, tools, companies, institutions |
| `10-sources/` | Source registry and processed source summaries |
| `11-public-exports/` | GitHub/LinkedIn drafts and portfolio-safe exports |
| `_templates/` | Reusable note templates |
| `_system/` | Vault index, operation log, guardrails |
| `_meta/` | Repository metadata, naming conventions, agent context |
| `.kiro/steering/` | Kiro agent operating instructions |
| `Clippings/` | Web clippings (excluded from public release) |

---

## How Notes Are Structured

Notes follow a typed system:

- **Atomic notes** — one reusable concept or idea
- **Molecule notes** — combine multiple atomic notes into workflows or explanations
- **MOC notes** — Maps of Content, navigation hubs for each domain
- **Entity notes** — people, tools, companies, institutions
- **Project notes** — portfolio project documentation
- **Source summaries** — processed summaries of source materials
- **Course notes** — Duke/Coursera/IBM certificate content (SOURCE_LOCKED)

All notes use:
- Lowercase hyphenated filenames (`my-note-name.md`)
- Obsidian `[[wikilinks]]` for internal linking
- Visibility labels: `PRIVATE_ONLY`, `PORTFOLIO_SAFE`, `SOURCE_LOCKED`, `PUBLIC_READY`
- Source citations: `(source: filename)`

---

## How Obsidian Is Used

This vault is maintained in [Obsidian](https://obsidian.md), a local Markdown editor with a knowledge graph view. Obsidian-specific features used:

- `[[wikilinks]]` for bidirectional linking between notes
- Graph view for visualizing note connections
- Templates for consistent note structure
- Folder-based organization with MOC navigation

The vault is Obsidian-compatible but all notes are plain Markdown — readable in any editor or on GitHub.

---

## Tool Integrations

| Tool | Role |
|---|---|
| **Obsidian** | Local knowledge graph editor |
| **GitHub** | Version control, remote access, portfolio visibility |
| **Kiro** | AI-assisted note creation, ingestion, and documentation |
| **NotebookLM** | Source enrichment — AI-assisted concept extraction from source materials |
| **Databricks** | Lab environment for data engineering and ML experiments |
| **Amazon Bedrock** | Future RAG deployment target — this vault is being prepared for Bedrock Knowledge Base ingestion |

---

## Future RAG Layer

Notes in this vault are being written with future RAG ingestion in mind:
- Concise, self-contained, factually grounded
- Structured with clear headings for chunking
- Source-cited for traceability
- Free of long AI-generated prose dumps

Target: Amazon Bedrock Knowledge Base for AI-assisted retrieval over this knowledge graph.

---

## What Is Excluded

Some content is intentionally excluded from this repository:

- `PRIVATE_ONLY` notes (personal plans, exam scheduling, career strategy)
- `SOURCE_LOCKED` content (verbatim Coursera/book material)
- Raw unprocessed source inbox (`10-sources/00-inbox/`)
- Obsidian local workspace state (`.obsidian/workspace.json`)
- Binary files (Excel workbooks, PDFs, images)

See `.gitignore` for the full exclusion list.

---

## Current Status

| Area | Status |
|---|---|
| Vault structure | ✅ Initialized |
| Core templates | ✅ Complete |
| AWS certification notes | ✅ Active |
| Mortgage Rate Intelligence project notes | ✅ Phase 1 complete |
| AI/ML concept notes | 🔄 Stubs — population in progress |
| NotebookLM ingestion workflow | ✅ Documented |
| RAG deployment | 🔮 Future |
| Public release | 🔒 Private — under review |

---

## Agent Instructions

Kiro and other AI agents working with this repository should read:
- `AGENTS.md` — operating instructions
- `_meta/kiro-web-agent-context.md` — Kiro Web context file
- `.kiro/steering/` — detailed workflow guides

---

*QuantPath LLM Wiki — built for compounding knowledge, not just note-taking.*
