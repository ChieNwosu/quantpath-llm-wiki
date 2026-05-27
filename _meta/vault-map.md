# Vault Map — QuantPath LLM Wiki

**Purpose**: High-level map of the vault structure, folder roles, and current population status.
**Last updated**: 2025-07-10

---

## Folder Structure

```
quantpath-llm-wiki/
├── 00-command-center/       Dashboard, roadmap, active priorities
├── 01-maps-of-content/      MOC navigation hubs (8 MOCs)
├── 02-ai-ml/                AI/ML concept notes (11 stubs)
├── 03-data-sql/             SQL and data engineering notes (10 stubs)
├── 04-aws-cloud/            AWS service notes + certification notes (13 files)
├── 05-quant-finance/        Quant finance + mortgage analytics (16 files)
│   └── mortgage-rate-time-series/  Phase 2 R analysis notes (5 files)
├── 06-databricks-labs/      Databricks and Spark notes (8 files)
├── 07-duke-coursera-wiki/   Course notes (8 files)
│   └── ibm-data-analytics-excel-r/  IBM certificate notes (3 files)
├── 08-projects/             Portfolio project notes (8 files)
│   └── mortgage-rate-intelligence/  Flagship project (8 files)
│       └── pm/              PM artifacts (5 files)
├── 09-entities/             Entity notes (9 files)
├── 10-sources/              Source registry and inbox
│   ├── 00-inbox/            Raw unprocessed sources (EXCLUDED from Git)
│   ├── source-registry/     source-file-index.md
│   └── source-summaries/    Processed summaries
├── 11-public-exports/       Portfolio-safe export drafts
├── Clippings/               Web clippings (EXCLUDED from Git — SOURCE_LOCKED)
├── _templates/              6 note templates
├── _system/                 Index, log, guardrails, ingestion guide
├── _meta/                   Repository metadata (this folder)
├── .kiro/steering/          Kiro agent steering files (6 files)
├── AGENTS.md                Kiro operating instructions
├── CLAUDE.md                Full operating instructions
├── README.md                Repository README
└── .gitignore               Git exclusion rules
```

---

## Population Status

| Folder | Files | Status |
|---|---|---|
| `00-command-center/` | 5 | Active — dashboard and roadmap have content |
| `01-maps-of-content/` | 8 | Mixed — moc-projects, moc-aws-cloud, moc-quant-finance active; others empty |
| `02-ai-ml/` | 11 | Stubs — most empty, need NotebookLM ingestion |
| `03-data-sql/` | 10 | Stubs — most empty |
| `04-aws-cloud/` | 13 | Active — certification notes and service stubs |
| `05-quant-finance/` | 16 | Active — mortgage analytics notes populated |
| `06-databricks-labs/` | 8 | Mixed — databricks.md has content; others empty |
| `07-duke-coursera-wiki/` | 8 + 3 | Mixed — IBM cert notes active; Duke notes empty |
| `08-projects/` | 8 + 13 | Active — mortgage-rate-intelligence fully documented |
| `09-entities/` | 9 | Stubs — most empty |
| `10-sources/` | Registry active | source-file-index.md populated |
| `11-public-exports/` | 5 | Stubs — most empty |
| `_templates/` | 6 | ✅ All populated |
| `_system/` | 7 | Active — index, log, guardrails populated |

---

## Key Entry Points

- **Start here**: `00-command-center/dashboard.md`
- **Domain navigation**: `01-maps-of-content/`
- **Flagship project**: `08-projects/mortgage-rate-intelligence/project-index.md`
- **AWS certification**: `04-aws-cloud/aws-certifications.md`
- **Source tracking**: `10-sources/source-registry/source-file-index.md`
- **Agent instructions**: `AGENTS.md`, `_meta/kiro-web-agent-context.md`
