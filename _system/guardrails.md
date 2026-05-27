# QuantPath LLM Wiki — Guardrails

**Purpose**: Security, privacy, and public export rules for the vault.
**Last updated**: 2025-07-10

---

## Visibility Labels

Every note should carry one of these labels:

| Label | Meaning |
|---|---|
| `PRIVATE_ONLY` | Personal reflections, career strategy, mentor conversations, application planning. Never export. |
| `PORTFOLIO_SAFE` | Can be adapted into GitHub, LinkedIn, README, or interview material. Requires human review before publishing. |
| `SOURCE_LOCKED` | Based on paid courses, books, copyrighted material, or private source excerpts. Summarize only — do not publish directly. |
| `PUBLIC_READY` | Reviewed, source-safe, privacy-safe, and ready for GitHub or LinkedIn. Human has approved. |

---

## Pre-Export Checklist

Before exporting any note to GitHub, LinkedIn, or any public platform:

- [ ] No private personal information (names, addresses, private conversations)
- [ ] No copied paid course text (Duke, Coursera, Packt, etc.)
- [ ] No API keys, credentials, tokens, or hidden configuration values
- [ ] No private documents or internal company materials
- [ ] Sources are listed and attributed
- [ ] Factual claims have been checked or flagged
- [ ] Written in my own voice — not a verbatim AI output
- [ ] Public value is clear — this adds something useful to a portfolio or reader
- [ ] Visibility label is `PUBLIC_READY` or `PORTFOLIO_SAFE`

---

## Source Handling Rules

### Immutable Raw Source Rule
Never rewrite or overwrite raw source files. Raw files in `10-sources/` are read-only inputs. Kiro may summarize them but must not modify them.

### Paid Course Content
- Do not copy lecture text, quiz questions, or assignment content verbatim.
- Summarize and transform into your own words.
- Mark all notes derived from paid courses as `SOURCE_LOCKED`.
- Store raw course notes in `10-sources/00-inbox/coursera-notes/` — do not move to permanent folders until summarized.

### AI-Generated Content
- Notes that are substantially AI-generated should be marked: `(AI-assisted: Kiro, YYYY-MM-DD)`
- Do not treat AI output as ground truth. Verify claims before marking as `Verified`.
- NotebookLM exports are AI outputs — flag claims that need verification.

---

## What Kiro Must Not Do

- Do not delete or overwrite raw source files.
- Do not mark notes as `PUBLIC_READY` — only the human can do that.
- Do not export or push content to GitHub or any external service.
- Do not include API keys, credentials, or secrets in any note.
- Do not copy paid course content verbatim into permanent notes.
- Do not create new top-level folders without explicit user approval.

---

## RAG / Bedrock Ingestion Guardrails

When preparing notes for Amazon Bedrock Knowledge Base ingestion:

- Exclude all `PRIVATE_ONLY` notes from the ingestion pipeline.
- Exclude all `SOURCE_LOCKED` notes unless they have been transformed into original summaries.
- Exclude `_system/`, `_templates/`, and `.kiro/` folders from ingestion.
- Include only notes from `02-ai-ml/` through `09-entities/` and `08-projects/`.
- Verify that no note contains credentials, private data, or copyrighted text before ingestion.

---

## Citation and Verification Rules

Every serious factual claim should be traceable to a source:

```
(source: filename-or-source-note)
```

If a claim needs checking:
```
[needs verification]
```

If two sources disagree:
```
Source conflict: Source A says X, while Source B says Y.
```

Separate facts from interpretation:
```markdown
## Verified Facts
## My Interpretation
## Open Questions
```
