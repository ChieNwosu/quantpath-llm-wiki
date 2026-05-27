# Source File Index — QuantPath LLM Wiki

**Purpose**: Running inventory of all source materials that feed the LLM Wiki.
**Maintained by**: Kiro (append on each ingestion operation)
**Last updated**: 2025-07-10

See `_system/notebooklm-to-llm-wiki-ingestion-guide.md` for the full ingestion workflow.
See `.kiro/steering/source-registry-policy.md` for registry maintenance rules.

---

## Status Key

| Status | Meaning |
|---|---|
| `Unprocessed` | File exists but no permanent notes created yet |
| `Partially Integrated` | Some notes created; more concepts remain |
| `Integrated` | All key concepts extracted; source summary exists |
| `Needs Review` | Notes created but contain unverified claims |

---

## Source Registry

| Source File | Current Location | Source Type | Status | Likely Wiki Domains | Notes |
|---|---|---|---|---|---|
| [[strands-agents-starter-lab]] | `08-projects/` | Lab Note | Partially Integrated | `02-ai-ml`, `04-aws-cloud`, `08-projects` | Agentic AI / MCP / Strands SDK lab note. Canonical project note created. Also registered here as source context for future agentic AI concept notes. |
| `book-notes.md` | `10-sources/` | Book Notes | Unprocessed | TBD | File exists but is currently empty. Populate when book sources are added. |
| `course-sources.md` | `10-sources/` | Course Note | Unprocessed | TBD | File exists but is currently empty. Populate with Duke/Coursera source references. |
| `datasets.md` | `10-sources/` | Dataset Reference | Unprocessed | TBD | File exists but is currently empty. Populate with dataset references. |
| `documentation-sources.md` | `10-sources/` | Documentation | Unprocessed | TBD | File exists but is currently empty. Populate with AWS/Databricks/SDK doc references. |
| `raw-documents.md` | `10-sources/` | Personal Note | Unprocessed | TBD | File exists but is currently empty. Intended for raw document references. |
| `source-summaries.md` | `10-sources/` | Personal Note | Unprocessed | TBD | File exists but is currently empty. May be superseded by `10-sources/source-summaries/` subfolder. |
| [[quantpath-databricks-mvp]] | `06-databricks-labs/` | Lab Note | Unprocessed | `06-databricks-labs`, `05-quant-finance` | MVP planning note. Currently empty — populate when Databricks lab work begins. |
| [[lab-log]] | `06-databricks-labs/` | Lab Note | Unprocessed | `06-databricks-labs` | Lab log for Databricks experiments. Currently empty. |
| [[coursera-packt-github]] | `07-duke-coursera-wiki/` | Course Note | Unprocessed | `07-duke-coursera-wiki` | Course source index. Review for integration into source registry. |
| [[course-source-index]] | `07-duke-coursera-wiki/` | Course Note | Unprocessed | `07-duke-coursera-wiki` | Course source index. Review for integration. |

---

## Notes on Empty Files

Several files in `10-sources/` and across the vault were created as placeholders but contain no content yet. These are marked `Unprocessed`. They should be populated as source material is gathered, or removed if they remain empty after the vault matures.

Files confirmed empty as of 2025-07-10:
- `10-sources/book-notes.md`
- `10-sources/course-sources.md`
- `10-sources/datasets.md`
- `10-sources/documentation-sources.md`
- `10-sources/raw-documents.md`
- `10-sources/source-summaries.md`
- `06-databricks-labs/quantpath-databricks-mvp.md`
- `06-databricks-labs/lab-log.md`
- Most `02-ai-ml/`, `03-data-sql/`, `04-aws-cloud/`, `05-quant-finance/` concept notes

---

## Recommended Moves (Pending User Approval)

| File | Current Location | Recommended Location | Reason |
|---|---|---|---|
| `Strands Agents Starter Lab.md` | vault root | `08-projects/strands-agents-starter-lab.md` | Naming convention (lowercase-hyphenated); belongs in projects folder. Canonical note already created there. Original can be deleted after review. |
