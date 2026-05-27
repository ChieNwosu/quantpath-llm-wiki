# QuantPath LLM Wiki — System Index

**Purpose**: Master index of vault structure, active notes, and system state.
**Last updated**: 2025-07-10 (rev 3)
**Vault status**: Initialization complete. AWS certification notes added. Reflections folder fully retired from all documentation.

---

## Vault Structure

```
llm-wiki/
├── 00-command-center/       6 files  — dashboard, roadmap, weekly plan, CLF-C02 study plan
├── 01-maps-of-content/      8 files  — MOCs (most empty, need population)
├── 02-ai-ml/               11 files  — concept notes (most empty)
├── 03-data-sql/            10 files  — concept notes (most empty)
├── 04-aws-cloud/           13 files  — concept notes + certification notes (active)
├── 05-quant-finance/       10 files  — concept notes (most empty)
├── 06-databricks-labs/      8 files  — lab notes (most empty)
├── 07-duke-coursera-wiki/   8 files  — course notes (mixed content)
├── 08-projects/             8 files  — project notes (most empty)
├── 09-entities/             9 files  — entity notes (content unknown)
├── 10-sources/              6 files + subfolders — source registry active
├── 11-public-exports/       5 files  — export drafts
├── 12-reflections/          REMOVED  — deleted (not relevant to development knowledge base)
├── _templates/              6 files  — note templates (all populated 2025-07-10)
├── _system/                 6 files  — system files
├── .kiro/steering/          6 files  — Kiro steering files (active)
├── AGENTS.md                         — Kiro operating instructions
└── CLAUDE.md                         — Full operating instructions
```

---

## Active System Files

| File | Status | Purpose |
|---|---|---|
| `CLAUDE.md` | Active | Full operating instructions for AI agents |
| `AGENTS.md` | Active | Kiro-specific operating instructions |
| `_system/index.md` | Active | This file |
| `_system/log.md` | Active | Append-only operation log |
| `_system/ingestion-rules.md` | Empty | Needs population from CLAUDE.md §6 |
| `_system/guardrails.md` | Active | Populated 2025-07-10 from CLAUDE.md §8 |
| `_system/evaluation-rules.md` | Empty | Needs population |
| `_system/public-export-checklist.md` | Empty | Needs population from CLAUDE.md §8 |
| `_system/notebooklm-to-llm-wiki-ingestion-guide.md` | Active | NotebookLM ingestion workflow |

---

## Active MOCs

| MOC | Status | Notes |
|---|---|---|
| `moc-projects.md` | Has content | Links to 6 project notes |
| `moc-ai-ml.md` | Empty | Needs population |
| `moc-aws-cloud.md` | Has content | Updated 2025-07-10 — certifications, full service list, CLF-C02 gaps |
| `moc-bedrock-rag.md` | Empty | Needs population |
| `moc-data-sql.md` | Empty | Needs population |
| `moc-databricks.md` | Empty | Needs population |
| `moc-duke-coursera.md` | Empty | Needs population |
| `moc-quant-finance.md` | Empty | Needs population |

---

## Notes With Content (Confirmed)

| Note | Folder | Status |
|---|---|---|
| `dashboard.md` | `00-command-center/` | Active |
| `databricks.md` | `06-databricks-labs/` | Has content |
| `moc-projects.md` | `01-maps-of-content/` | Has content |
| `CLAUDE.md` | root | Active — full instructions |
| `AGENTS.md` | root | Active — Kiro instructions |
| `aws-certifications.md` | `04-aws-cloud/` | Active — created 2025-07-10 |
| `aws-certified-cloud-practitioner-clf-c02.md` | `04-aws-cloud/` | Active — created 2025-07-10 |
| `clf-c02-june-17-study-plan.md` | `00-command-center/` | Active — PRIVATE_ONLY |

---

## Source Registry

Active registry: [[source-file-index]] (`10-sources/source-registry/source-file-index.md`)

Sources currently tracked: 11 entries (most unprocessed/empty placeholders)
Sources with content: `Strands Agents Starter Lab.md` (partially integrated)

---

## Priority Actions

1. Populate empty MOCs as concept notes are created (AWS MOC now active)
2. Create CLF-C02 priority concept notes: `shared-responsibility-model`, `aws-well-architected-framework`, `cloud-computing`, `ec2`
3. Begin NotebookLM ingestion workflow — AWS whitepapers are ideal first source
4. Decide whether to keep or delete the original `Strands Agents Starter Lab.md` at vault root
