# Naming Conventions — QuantPath LLM Wiki

**Purpose**: Reference for consistent file and folder naming across the vault.
**Last updated**: 2025-07-10

---

## Filenames

| Rule | Example |
|---|---|
| Lowercase only | `rag.md` not `RAG.md` |
| Hyphens for spaces | `sharpe-ratio.md` not `sharpe_ratio.md` or `SharpeRatio.md` |
| No spaces | `project-index.md` not `project index.md` |
| No underscores (except system files) | `moc-ai-ml.md` not `moc_ai_ml.md` |
| Descriptive, not generic | `aws-certified-cloud-practitioner-clf-c02.md` not `cert-notes.md` |

**Exceptions** (uppercase by convention):
- `AGENTS.md`
- `CLAUDE.md`
- `README.md`

---

## Folder Names

Same rules as filenames:
- Lowercase with hyphens
- Numbered prefixes for top-level domain folders: `02-ai-ml/`, `04-aws-cloud/`
- Descriptive subfolder names: `mortgage-rate-time-series/`, `ibm-data-analytics-excel-r/`

---

## Note Title (H1)

The H1 title inside a note does not need to match the filename exactly, but should be closely related:

- File: `refinance-break-even.md`
- Title: `# Refinance Break-Even`

---

## Wikilink Targets

Wikilinks use the filename without the `.md` extension:
- `[[refinance-break-even]]` links to `refinance-break-even.md`
- `[[project-index]]` links to `project-index.md`
- Do not include folder paths unless disambiguation is needed

---

## Date Format

Use ISO 8601 in all notes: `YYYY-MM-DD`
Example: `**Last updated**: 2025-07-10`

---

## Visibility Labels

Always use exact label text (case-sensitive):
- `PRIVATE_ONLY`
- `PORTFOLIO_SAFE`
- `SOURCE_LOCKED`
- `PUBLIC_READY`

---

## Status Labels (for projects and phases)

- `✅ Complete`
- `🔄 In Progress`
- `🗓 Planned`
- `🔮 Future`
