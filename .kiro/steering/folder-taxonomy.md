---
inclusion: always
---

# Folder Taxonomy — QuantPath LLM Wiki

## Top-Level Structure

```
llm-wiki/
├── 00-command-center/       # Dashboard, weekly plan, active projects, roadmap
├── 01-maps-of-content/      # MOC navigation hubs by domain
├── 02-ai-ml/                # AI/ML concept notes
├── 03-data-sql/             # SQL, analytics, data engineering notes
├── 04-aws-cloud/            # AWS service and cloud architecture notes
├── 05-quant-finance/        # Quantitative finance concept notes
├── 06-databricks-labs/      # Databricks, Spark, notebook lab notes
├── 07-duke-coursera-wiki/   # Duke/Coursera course notes
├── 08-projects/             # Portfolio project documentation
├── 09-entities/             # People, tools, companies, institutions, datasets
├── 10-sources/              # Source materials, summaries, registry
│   ├── 00-inbox/            # Unprocessed incoming source material
│   │   ├── notebooklm-exports/
│   │   ├── web-clips/
│   │   └── coursera-notes/
│   ├── source-summaries/    # Processed source summary notes
│   └── source-registry/     # Source file index and tracking
├── 11-public-exports/       # GitHub-safe notes, README drafts, LinkedIn drafts
├── _templates/              # Reusable note templates
├── _system/                 # Index, log, guardrails, ingestion rules
├── .kiro/steering/          # Kiro steering files (this folder)
├── AGENTS.md                # Kiro operating instructions
└── CLAUDE.md                # Full operating instructions (legacy, still valid)
```

## Folder Routing Rules

| If the note is about... | Route to |
|---|---|
| A single AI/ML concept (RAG, embeddings, classification) | `02-ai-ml/` |
| SQL syntax, data modeling, pipelines, ETL | `03-data-sql/` |
| An AWS service (S3, Bedrock, Lambda, Glue) | `04-aws-cloud/` |
| A quant finance concept (Sharpe ratio, volatility, DeFi) | `05-quant-finance/` |
| A Databricks lab, Spark concept, or notebook workflow | `06-databricks-labs/` |
| A Duke or Coursera course module or concept | `07-duke-coursera-wiki/` |
| A portfolio project (building, documenting, publishing) | `08-projects/` |
| A person, company, tool, institution, or dataset | `09-entities/` |
| A raw source, source summary, or captured material | `10-sources/` |
| A GitHub README draft, LinkedIn post, or portfolio page | `11-public-exports/` |
| A navigation hub linking multiple notes in a domain | `01-maps-of-content/` |
| A weekly plan, active priority, or dashboard item | `00-command-center/` |

## Existing MOCs

| MOC File | Domain |
|---|---|
| `moc-ai-ml.md` | AI and machine learning |
| `moc-aws-cloud.md` | AWS and cloud infrastructure |
| `moc-bedrock-rag.md` | Bedrock and RAG specifically |
| `moc-data-sql.md` | Data and SQL |
| `moc-databricks.md` | Databricks platform |
| `moc-duke-coursera.md` | Duke/Coursera courses |
| `moc-projects.md` | Portfolio projects |
| `moc-quant-finance.md` | Quantitative finance |

## Notes on Subfolder Creation

- Do not create new top-level folders without explicit user approval.
- Subfolders within `10-sources/` are pre-approved: `00-inbox/`, `source-summaries/`, `source-registry/`.
- Other subfolders may be created when 5+ notes clearly belong together and the grouping adds navigational value.
- Always explain the reason before creating a new subfolder.
