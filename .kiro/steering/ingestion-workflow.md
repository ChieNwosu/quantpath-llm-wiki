---
inclusion: always
---

# Ingestion Workflow — QuantPath LLM Wiki

This file describes the step-by-step process Kiro follows when the user provides a new source for ingestion into the wiki.

## Trigger

The user drops a file into `10-sources/00-inbox/` (or one of its subfolders) and asks Kiro to process it, OR pastes content directly into the chat.

## Step-by-Step Process

### Step 1 — Read and Classify the Source

- Read the full source file.
- Identify the source type: NotebookLM export / web clip / course note / lab note / book excerpt / documentation / personal note / AI output.
- Identify the primary domain(s): AI/ML, Data/SQL, AWS/Cloud, Quant Finance, Databricks, Duke/Coursera, Agentic AI, Projects.
- Note whether the source is from a paid/copyrighted resource (affects visibility label).

### Step 2 — Create a Source Summary Note

If the source is substantial (more than a few paragraphs), create a source summary note at:
`10-sources/source-summaries/[source-name]-summary.md`

Use the source summary template from `_templates/source-summary-template.md`:
- Source type, original file/link, date added, status
- Summary (2–5 sentences)
- Key ideas (bullet list)
- Potential wiki pages to create
- Portfolio or project connections
- Verification notes

### Step 3 — Extract Permanent Note Candidates

From the source, identify:
- **Atomic notes**: single concepts worth capturing (e.g., "what is RAG", "Sharpe ratio formula")
- **Molecule notes**: workflows or multi-concept explanations (e.g., "RAG pipeline architecture")
- **Entity notes**: new people, tools, companies, or datasets mentioned
- **Project connections**: anything that connects to an existing or new portfolio project

List these candidates before creating them. For large sources, confirm with the user before creating more than ~5 new notes.

### Step 4 — Create or Update Permanent Notes

For each candidate:
- Check if a note already exists in the correct domain folder. If yes, update it rather than creating a duplicate.
- If creating new: use the correct template, route to the correct folder, follow naming convention (lowercase-hyphenated).
- Add `**Sources**:` field pointing back to the source file.
- Add `(source: filename)` inline citations for specific claims.
- Add wikilinks to related existing notes.

### Step 5 — Update MOCs

For each domain touched by the ingestion:
- Open the relevant MOC in `01-maps-of-content/`.
- Add wikilinks to any new notes created.
- Place them in the appropriate section of the MOC.

### Step 6 — Update the Source Registry

Add or update the source entry in:
`10-sources/source-registry/source-file-index.md`

Update the Status column:
- `Unprocessed` → `Partially Integrated` (if some notes created but more remain)
- `Unprocessed` → `Integrated` (if fully processed)

### Step 7 — Append to System Log

Append a dated entry to `_system/log.md`:

```markdown
## YYYY-MM-DD — Ingested: [Source Name]

- Source type: [type]
- Notes created: [[note-one]], [[note-two]]
- Notes updated: [[existing-note]]
- MOCs updated: [[moc-name]]
- Source registry: updated
```

### Step 8 — Report to User

Summarize what was done:
- Source classified as: [type]
- Notes created: [list]
- Notes updated: [list]
- MOCs updated: [list]
- Any items that need user review or verification

## Special Cases

### NotebookLM Exports
- These are AI-enriched summaries. Treat as `AI Output` source type.
- Mark notes derived from them with `(source: notebooklm-export-filename)`.
- Do not treat NotebookLM output as ground truth — flag claims that need verification.

### Paid Course Content
- Do not copy verbatim. Summarize and transform into your own words.
- Mark notes as `SOURCE_LOCKED` visibility.
- Store raw course notes in `10-sources/00-inbox/coursera-notes/` — do not move to permanent folders until summarized.

### Lab Notes / Project Context
- Lab notes that document hands-on work belong in `08-projects/` or `06-databricks-labs/`.
- If a lab note also functions as a source for concept notes, add it to the source registry.

### Web Clips
- Store raw clips in `10-sources/00-inbox/web-clips/`.
- Create a source summary before extracting permanent notes.
- Verify claims from web clips before marking as `Verified`.
