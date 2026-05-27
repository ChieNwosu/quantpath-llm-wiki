---
inclusion: always
---

# Source Registry Policy — QuantPath LLM Wiki

## Purpose

The source registry is a running inventory of all source materials that feed the LLM Wiki. It ensures traceability, prevents duplicate processing, and supports future RAG/Bedrock ingestion audits.

## Registry Location

```
10-sources/source-registry/source-file-index.md
```

## Registry Table Format

The registry uses this table structure:

| Source File | Current Location | Source Type | Status | Likely Wiki Domains | Notes |
|---|---|---|---|---|---|

### Column Definitions

- **Source File**: The filename (with wikilink if it exists in the vault).
- **Current Location**: The folder path where the file currently lives.
- **Source Type**: One of: `NotebookLM Export`, `Web Clip`, `Course Note`, `Book Notes`, `Documentation`, `Lab Note`, `AI Output`, `Personal Note`, `Dataset Reference`.
- **Status**: One of: `Unprocessed`, `Partially Integrated`, `Integrated`, `Needs Review`.
- **Likely Wiki Domains**: The domain folders this source feeds (e.g., `02-ai-ml`, `04-aws-cloud`).
- **Notes**: Any relevant context — e.g., "paid course content, SOURCE_LOCKED", "NotebookLM enriched", "needs verification".

## When to Update the Registry

Update `source-file-index.md` whenever:
- A new source file is added to `10-sources/00-inbox/` or any subfolder.
- A source is processed and notes are created from it (update Status).
- A source is moved to a different location (update Current Location).
- A source is determined to be a duplicate or superseded (add note).

## Status Lifecycle

```
Unprocessed → Partially Integrated → Integrated
                                   ↘ Needs Review (if claims need verification)
```

- **Unprocessed**: File exists in the vault but no permanent notes have been created from it yet.
- **Partially Integrated**: Some notes created, but more concepts remain to be extracted.
- **Integrated**: All key concepts have been extracted into permanent notes. Source summary exists.
- **Needs Review**: Notes were created but contain unverified claims or the source itself needs re-evaluation.

## What Counts as a Source File

Add to the registry if the file is:
- A NotebookLM-enriched export
- A web clip or article saved for reference
- A course note or lecture summary
- A book excerpt or reading note
- A lab note that functions as context for concept notes
- A project planning document that feeds wiki content
- Any uploaded or pasted material intended to become permanent notes

Do NOT add to the registry:
- Permanent wiki notes (atomic, molecule, entity, project notes)
- MOC notes
- Template files
- System files (`_system/`, `_templates/`)
- The dashboard or command center files

## Immutable Raw Source Rule

Never overwrite or delete raw source files. If a source needs correction, create a new version with a `-v2` suffix and note the relationship in the registry.

Raw source files in `10-sources/00-inbox/` should not be moved to permanent folders until they have been summarized. The summary goes to `10-sources/source-summaries/`; the raw file stays in the inbox or is archived.
