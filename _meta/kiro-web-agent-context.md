# Kiro Web Agent Context — QuantPath LLM Wiki

**Purpose**: Context file for Kiro Web. Read this before modifying any notes in this repository.
**Last updated**: 2025-07-10

---

## What This Repository Is

This is the **QuantPath LLM Wiki** — a personal knowledge operating system maintained in Obsidian and version-controlled with Git. It is a structured Markdown knowledge graph covering AI/ML, data engineering, AWS/cloud, quantitative finance, Databricks, Duke/Coursera coursework, and portfolio projects.

The vault is being prepared for future deployment as an Amazon Bedrock Knowledge Base for RAG-based AI assistance.

Full operating instructions: `AGENTS.md` (root)
Detailed workflow guides: `.kiro/steering/`

---

## How to Modify Notes Safely

### Always do
- Read the existing note before modifying it
- Preserve all `[[wikilinks]]` — do not convert them to plain text or URLs
- Follow the lowercase-hyphenated filename convention: `my-note-name.md`
- Add `**Sources**:` and `**Last updated**:` fields when creating new notes
- Use the correct template from `_templates/` for the note type
- Update the relevant MOC in `01-maps-of-content/` when creating a new permanent note
- Append a log entry to `_system/log.md` after significant operations

### Never do
- Delete or overwrite raw source files in `10-sources/`
- Modify files marked `PRIVATE_ONLY` — skip them entirely
- Copy paid course content verbatim into permanent notes
- Mark notes as `PUBLIC_READY` — only the human can do that
- Create new top-level folders without explicit user approval
- Push or export content to GitHub or any external service
- Add API keys, credentials, or secrets to any note

---

## How to Preserve Obsidian Wikilinks

Obsidian uses `[[note-name]]` syntax for internal links. These are **not** standard Markdown links.

- Always write internal links as `[[note-name]]` — not `[note-name](path/to/note.md)`
- The link target is the filename without the `.md` extension
- Links are case-insensitive in Obsidian but use lowercase by convention
- Do not add folder paths inside wikilinks unless disambiguation is needed: `[[note-name]]` not `[[folder/note-name]]`
- When creating a new note that should be linked from existing notes, add the wikilink to the relevant MOC and any related notes

---

## How to Create Evergreen Notes

Evergreen notes are permanent, reusable concept notes that stand on their own.

**Routing by content type:**

| Content | Folder |
|---|---|
| AI/ML concept | `02-ai-ml/` |
| SQL / data engineering | `03-data-sql/` |
| AWS service or cloud concept | `04-aws-cloud/` |
| Quant finance concept | `05-quant-finance/` |
| Databricks / Spark | `06-databricks-labs/` |
| Course note | `07-duke-coursera-wiki/` |
| Portfolio project | `08-projects/` |
| Person / tool / company | `09-entities/` |

**Required fields for every permanent note:**
```markdown
**Summary**: One or two sentences.
**Type**: Atomic / Molecule / Entity / Project / MOC
**Sources**: (source: filename) or external reference
**Last updated**: YYYY-MM-DD
**Visibility**: PORTFOLIO_SAFE / PRIVATE_ONLY / SOURCE_LOCKED / PUBLIC_READY
```

Use `_templates/concept-note-template.md` as the starting point for atomic notes.

---

## How to Avoid Touching Private/Excluded Content

Files and folders that should never be modified or read for content extraction:

| Path | Reason |
|---|---|
| `00-command-center/clf-c02-june-17-study-plan.md` | PRIVATE_ONLY — personal exam plan |
| `08-projects/mortgage-rate-intelligence/pm/retrospective.md` | PRIVATE_ONLY — personal reflection |
| `10-sources/00-inbox/` | Raw unprocessed sources — do not modify |
| `Clippings/` | SOURCE_LOCKED — verbatim course content |
| `11-public-exports/interview-talking-points.md` | PRIVATE_ONLY — career content |
| `.obsidian/workspace.json` | Local UI state — do not modify |

If a note has `**Visibility**: PRIVATE_ONLY` in its header, skip it entirely.

---

## How to Structure MLOps Notes

MLOps notes belong in `02-ai-ml/` or `06-databricks-labs/` depending on focus:

- **Concept-level MLOps** (model versioning, feature stores, monitoring, drift detection) → `02-ai-ml/`
- **Platform-level MLOps** (Databricks MLflow, Delta Lake, Spark pipelines) → `06-databricks-labs/`

MLOps notes should follow the atomic note template and include:
- What the concept is
- Why it matters for production ML systems
- How it connects to AWS (SageMaker, Bedrock) or Databricks
- A practical example or code sketch
- Links to related notes and the `moc-ai-ml` or `moc-databricks` MOC

---

## How to Write GitHub-Compatible Markdown

All notes in this vault are plain Markdown and render correctly on GitHub with these conventions:

- Use `#` for H1 (note title), `##` for sections, `###` for subsections
- Use fenced code blocks with language tags: ` ```python `, ` ```sql `, ` ```r `
- Use standard Markdown tables (pipe syntax)
- Use `- ` for bullet lists, `1. ` for numbered lists
- **Exception**: `[[wikilinks]]` render as plain text on GitHub — this is expected and acceptable. The links work in Obsidian; GitHub shows them as text.
- Avoid Obsidian-specific callout syntax (`> [!note]`) unless you confirm GitHub renders it

---

## How to Support Future RAG Ingestion

Notes destined for Amazon Bedrock Knowledge Base ingestion should be:

1. **Concise** — avoid long AI-generated prose dumps; prefer structured bullet points
2. **Self-contained** — each note should be understandable without reading other notes
3. **Factually grounded** — cite sources; flag unverified claims with `[needs verification]`
4. **Well-structured** — clear H2/H3 headings enable better chunking
5. **Source-cited** — use `(source: filename)` inline citations

**Exclude from RAG ingestion:**
- `PRIVATE_ONLY` notes
- `SOURCE_LOCKED` notes (unless transformed into original summaries)
- `_system/`, `_templates/`, `.kiro/` folders
- `00-command-center/` operational notes

**Include in RAG ingestion:**
- `02-ai-ml/` through `09-entities/`
- `08-projects/` (project notes, not PM artifacts)
- `01-maps-of-content/` (MOCs as navigation context)

---

## Key Files to Read First

Before starting any significant operation in this vault:

1. `AGENTS.md` — full operating instructions
2. `_system/index.md` — vault structure and current state
3. `_system/log.md` — recent operations
4. `10-sources/source-registry/source-file-index.md` — source inventory
5. The relevant MOC for the domain you're working in
