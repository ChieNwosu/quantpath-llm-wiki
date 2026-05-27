# AGENTS.md — Kiro Operating Instructions for the QuantPath LLM Wiki

This file instructs Kiro and any future agentic tools how to maintain, extend, and operate within this Obsidian vault.

---

## 1. What This Vault Is

This is the **QuantPath LLM Wiki**: a personal, AI-assisted knowledge base inspired by Andrej Karpathy's LLM Wiki pattern. It is maintained in Obsidian as a Markdown knowledge graph.

The vault covers:
- AI/ML concepts, model evaluation, RAG, embeddings, guardrails
- Data analytics, SQL, data engineering, pipelines
- AWS/cloud infrastructure (S3, Glue, Athena, Bedrock, Lambda, IAM)
- Quantitative finance (returns, volatility, risk, portfolio theory, DeFi)
- Databricks labs and Spark workflows
- Duke/Coursera specialization course notes
- Agentic AI, MCP, Strands Agents SDK, Kiro
- Portfolio projects and GitHub documentation
- Long-term QuantPath OS development

The vault is being prepared for future deployment as an **Amazon Bedrock Knowledge Base** for RAG-based AI assistance.

---

## 2. Core Operating Rules

### 2.1 Note Links
- Always use Obsidian `[[wikilinks]]` to connect notes.
- Never use bare URLs for internal references.
- When creating or updating a note, add relevant wikilinks to related concept notes, MOCs, entity notes, and project notes.

### 2.2 Naming Convention
- All note filenames must be **lowercase with hyphens**: `my-note-name.md`
- No spaces, no camelCase, no underscores in filenames.
- Folder names follow the same convention.

### 2.3 Folder Routing
Route new permanent notes to the correct domain folder:

| Content Type | Folder |
|---|---|
| AI/ML concepts | `02-ai-ml/` |
| SQL, data analytics, pipelines | `03-data-sql/` |
| AWS/cloud services | `04-aws-cloud/` |
| Quant finance concepts | `05-quant-finance/` |
| Databricks, Spark, notebooks | `06-databricks-labs/` |
| Duke/Coursera course notes | `07-duke-coursera-wiki/` |
| Portfolio projects | `08-projects/` |
| People, tools, companies, institutions | `09-entities/` |
| Source materials, summaries, raw notes | `10-sources/` |
| GitHub/LinkedIn/portfolio exports | `11-public-exports/` |
| Navigation hubs | `01-maps-of-content/` |
| Weekly plans, active priorities | `00-command-center/` |

### 2.4 MOC Updates
- When a new permanent note is created in a domain folder, check whether the relevant MOC in `01-maps-of-content/` should be updated.
- Add a wikilink to the new note in the appropriate MOC section.
- Do not create new MOCs without justification. Prefer updating existing ones.

### 2.5 System Log
- After any significant wiki-building operation (ingestion, bulk note creation, structural change), append a dated entry to `_system/log.md`.
- Format: `## YYYY-MM-DD — [Operation Summary]` followed by a brief bullet list of what was created, updated, or changed.

### 2.6 Source Discipline
- Never overwrite or rewrite raw source files.
- Raw/source material lives in `10-sources/` and its subfolders.
- Summarize sources; do not copy them verbatim into permanent notes.
- Every permanent note that draws from a source should include a `(source: filename)` citation.
- When a new source is processed, add it to `10-sources/source-registry/source-file-index.md`.

### 2.7 Provenance Preservation
- When creating notes from source material, always record where the content came from.
- Use the `**Sources**:` field in note frontmatter or headers.
- If a note is AI-generated or AI-assisted, note that clearly.

### 2.8 Folder Creation Policy
- Do not create new top-level folders without explicit user approval.
- Subfolders within existing folders may be created when there are 5+ notes that clearly belong together.
- Always explain the reason for a new subfolder before creating it.

### 2.9 RAG Readiness
- Keep notes concise, self-contained, and factually grounded.
- Avoid long AI-generated prose dumps. Prefer structured, chunked content.
- Each note should be understandable without reading other notes (though wikilinks are encouraged).
- This supports future chunking and embedding for Bedrock Knowledge Base ingestion.

---

## 3. Note Type Reference

| Note Type | Purpose | Template |
|---|---|---|
| Atomic | One reusable concept or idea | `_templates/concept-note-template.md` |
| Molecule | Combines multiple atomic notes | `_templates/concept-note-template.md` |
| MOC | Navigation hub for a domain | `01-maps-of-content/` |
| Entity | Person, tool, company, course, dataset | `_templates/entity-note-template.md` |
| Project | Portfolio project documentation | `_templates/project-note-template.md` |
| Source Summary | Summary of a source file | `_templates/source-summary-template.md` |
| Course Note | Duke/Coursera course content | `_templates/course-note-template.md` |

---

## 4. Ingestion Workflow Summary

When the user provides a new source (NotebookLM export, web clip, course note, lab note):

1. Read the source.
2. Identify source type and domain.
3. Create a source summary note in `10-sources/source-summaries/` if the source is substantial.
4. Extract permanent note candidates (atomic, molecule, entity, project).
5. Create or update notes in the correct domain folders.
6. Add wikilinks between new and existing notes.
7. Update relevant MOCs.
8. Add the source to `10-sources/source-registry/source-file-index.md`.
9. Append a log entry to `_system/log.md`.

Full ingestion guide: `_system/notebooklm-to-llm-wiki-ingestion-guide.md`

---

## 5. What Kiro Should NOT Do

- Do not rewrite or delete raw source files.
- Do not create sweeping folder restructures without user approval.
- Do not add tags prolifically — this vault uses wikilinks, not tags, for organization.
- Do not copy paid course content verbatim into notes.
- Do not mark notes as `PUBLIC_READY` without user review.
- Do not make assumptions about what the user wants to publish.

---

## 6. Key System Files

| File | Purpose |
|---|---|
| `CLAUDE.md` | Full operating instructions (legacy, still valid) |
| `AGENTS.md` | This file — Kiro-facing operating instructions |
| `_system/index.md` | Vault index and structure map |
| `_system/log.md` | Append-only operation log |
| `_system/ingestion-rules.md` | Detailed ingestion rules |
| `_system/guardrails.md` | Security and public export guardrails |
| `10-sources/source-registry/source-file-index.md` | Running inventory of source materials |
| `_system/notebooklm-to-llm-wiki-ingestion-guide.md` | NotebookLM → Kiro → Obsidian workflow |

---

## 7. Steering Files

Detailed workflow guides live in `.kiro/steering/`:

| File | Purpose |
|---|---|
| `llm-wiki-purpose.md` | Vault purpose and goals |
| `folder-taxonomy.md` | Folder structure and routing rules |
| `note-formatting-rules.md` | Note format standards |
| `ingestion-workflow.md` | Step-by-step ingestion process |
| `folder-expansion-policy.md` | When and how to create new folders |
| `source-registry-policy.md` | How to maintain the source registry |
