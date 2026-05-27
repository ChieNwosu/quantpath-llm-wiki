# NotebookLM → Kiro → Obsidian Ingestion Guide

**Purpose**: Step-by-step workflow for converting NotebookLM-enriched notes into permanent wiki knowledge.
**Type**: System guide
**Last updated**: 2025-07-10

---

## Overview

This workflow turns raw learning material into structured, interlinked wiki notes using NotebookLM for enrichment and Kiro for ingestion.

```
Source Material
    ↓
NotebookLM (enrich, summarize, extract concepts)
    ↓
10-sources/00-inbox/notebooklm-exports/  (save enriched output)
    ↓
Kiro (classify → summarize → create notes → link → update MOCs → log)
    ↓
Permanent Wiki Notes (02-ai-ml/, 03-data-sql/, etc.)
```

---

## Step 1 — Capture Source Material

Gather your raw material. This could be:
- A course lecture or reading
- AWS/Databricks/SDK documentation
- A book chapter or article
- Your own notes from a lab or project

---

## Step 2 — Enrich with NotebookLM

1. Upload or paste the source material into NotebookLM.
2. Use NotebookLM to:
   - Generate a summary
   - Extract key concepts and definitions
   - Identify connections to other topics
   - Generate study questions or explanations
3. Copy the enriched output (summary + key concepts + explanations).

---

## Step 3 — Save to the Inbox

Save or paste the NotebookLM output as a Markdown file in:

```
10-sources/00-inbox/notebooklm-exports/
```

**Naming convention**: `YYYY-MM-DD-topic-name.md`
Example: `2025-07-10-rag-architecture.md`

Include at the top of the file:
```markdown
# NotebookLM Export: [Topic Name]

**Date**: YYYY-MM-DD
**Original source**: [Course name / book / URL / personal notes]
**NotebookLM session**: [brief description of what you asked]
**Domain**: [AI/ML / Data / AWS / Quant Finance / Databricks / etc.]
```

---

## Step 4 — Ask Kiro to Process It

Use the reusable prompt below. Drop it into Kiro after saving your file to the inbox.

---

## Reusable Kiro Ingestion Prompt

Copy and paste this prompt each time you add a new NotebookLM export:

---

```
I've added a new NotebookLM-enriched note to the inbox:
10-sources/00-inbox/notebooklm-exports/[FILENAME].md

Please process it following the QuantPath LLM Wiki ingestion workflow:

1. Read and classify the source (type, domain, paid/free).
2. Create a source summary note in 10-sources/source-summaries/.
3. Identify permanent note candidates (atomic, molecule, entity, project).
4. Tell me what notes you plan to create or update before making changes.
5. After I confirm, create or update the notes in the correct domain folders.
6. Add wikilinks to related existing notes.
7. Update the relevant MOCs in 01-maps-of-content/.
8. Add the source to 10-sources/source-registry/source-file-index.md.
9. Append a log entry to _system/log.md.
10. Give me a summary of everything created, updated, and flagged for review.
```

---

## Step 5 — Review Kiro's Plan

Before Kiro creates notes, it will list:
- The source summary it plans to create
- The permanent notes it plans to create or update
- Any claims it's flagging for verification
- Any content it's marking `SOURCE_LOCKED`

Review the plan and confirm or adjust before proceeding.

---

## Step 6 — Review the Output

After ingestion, check:
- [ ] Notes are in the correct folders
- [ ] Filenames follow lowercase-hyphenated convention
- [ ] Wikilinks connect to related notes
- [ ] MOCs are updated
- [ ] Source registry is updated
- [ ] Log entry is appended
- [ ] Visibility labels are appropriate
- [ ] No paid course content was copied verbatim

---

## Tips for Better NotebookLM Exports

- Ask NotebookLM to "explain this concept as if teaching it" — produces better atomic note content than raw summaries.
- Ask for "connections to related concepts" — helps Kiro identify wikilink targets.
- Ask for "practical examples" — these become the `## Example` sections in atomic notes.
- Ask for "potential interview questions" — these feed the `## Interview Explanation` sections.
- Keep each export focused on one topic or one course module. Smaller, focused exports produce better notes than large dumps.

---

## Related Files

- [[AGENTS.md]] — Kiro operating instructions
- [[ingestion-workflow]] — Detailed step-by-step ingestion process (`.kiro/steering/`)
- [[source-registry-policy]] — How to maintain the source registry (`.kiro/steering/`)
- [[source-file-index]] — Running source inventory (`10-sources/source-registry/`)
- [[_system/log]] — Operation log
