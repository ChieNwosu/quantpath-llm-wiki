# MLOps Vault Practices

**Summary**: Operational guide for maintaining, growing, and integrating the MLOps knowledge layer — including conventions for converting learning into durable knowledge, RAG-readiness practices, and GitHub-compatible documentation standards.
**Type**: Meta / process note
**Status**: Active
**Last updated**: 2026-05-27
**Visibility**: PORTFOLIO_SAFE

---

## 1. Converting KodeKloud Learning into Evergreen Notes

KodeKloud courses produce procedural knowledge ("how to do X"). Evergreen notes require conceptual knowledge ("why X matters, when it fails, how it connects"). The conversion process:

### Conversion Framework

```
KodeKloud Lab Exercise
        │
        ▼
┌─────────────────────────────────────────┐
│  Ask:                                    │
│  1. What concept does this exercise      │
│     demonstrate?                         │
│  2. When would this fail in production?  │
│  3. What systems depend on this?         │
│  4. What does this replace or improve?   │
│  5. How does this connect to existing    │
│     vault knowledge?                     │
└─────────────────────────────────────────┘
        │
        ▼
Evergreen Note (concept-centered, not tutorial-centered)
```

### Do / Don't

| Do | Don't |
|---|---|
| Extract the *principle* behind the lab | Copy-paste lab steps as a tutorial |
| Add failure modes and risks | Document only the happy path |
| Connect to AWS/Databricks equivalents | Treat tools as isolated islands |
| Add governance and production context | Write notes only useful for passing the lab |
| Use atomic note structure | Create monolithic "everything about Docker" notes |

### Example Transformation

**KodeKloud lab**: "Create a multi-stage Docker build"

**Evergreen note**: `docker-layer-caching.md` — covering why layer ordering matters, cache invalidation rules, CI/CD integration, failure modes, and production optimization patterns.

---

## 2. Transforming Operational Exercises into Durable Knowledge

### From Exercise to Insight

Every operational exercise (hands-on lab, debugging session, incident response) produces two types of value:

1. **Procedural memory** (decays without practice) — "I ran these commands"
2. **Conceptual understanding** (durable) — "I understand why this architecture works/fails"

Vault notes should capture type 2, referencing type 1 only as illustrative examples.

### Post-Exercise Capture Template

After completing any operational exercise, create or update notes using:

```markdown
## What I Did
[Brief description — 1-2 sentences]

## What I Learned (conceptual)
[The durable insight — systems relationship, failure mode, architectural principle]

## What Would Break This
[Failure modes, edge cases, assumptions that might not hold]

## Connection to Production
[How this applies in real infrastructure, not just lab environments]

## Related Notes
[Wikilinks to existing vault knowledge]
```

---

## 3. Integrating Databricks Engineering Journals

### Journal-to-Note Pipeline

Databricks exploration produces notebooks, experiment logs, and informal observations. Convert these into vault knowledge:

1. **Weekly review**: Scan Databricks notebooks for conceptual insights
2. **Extract principles**: What did you learn about Delta Lake behavior, Spark optimization, MLflow patterns?
3. **Create/update atomic notes**: One concept per note, linked to existing knowledge
4. **Cross-reference**: Link to `06-databricks-labs/lab-log.md` for chronological context

### Databricks-Specific Note Patterns

- **Platform behavior notes**: "Delta Lake does X when Y" (not "how to use Delta Lake")
- **Performance observations**: "Spark partitioning affects Z because..." (not "set partition count to N")
- **Integration patterns**: "MLflow + Unity Catalog interaction when..." (architectural understanding)

---

## 4. RAG-Readiness Practices

### Design for Machine Consumption

Every note should be parseable by embedding models and retrievable by semantic search. This requires:

### Structural Requirements

| Requirement | Rationale |
|---|---|
| Clear H1 title matching filename | Chunk identification and citation |
| YAML frontmatter with tags/aliases | Metadata filtering in vector search |
| Self-contained sections under H2/H3 | Each section is a valid retrieval chunk |
| Explicit definitions early in note | Embedding models weight opening content |
| Concrete examples after abstractions | Retrieval quality improves with specificity |
| Related Notes section | Graph traversal for multi-hop retrieval |

### Embedding-Friendly Writing

- **First paragraph**: Define the concept in plain, complete terms (this becomes the "summary embedding")
- **Section independence**: Each H2 section should be understandable without reading the entire note
- **Avoid pronouns without antecedents**: "It does X" is bad for chunks; "The model registry does X" is good
- **Include key terms**: Use canonical terminology that users would search for

### Anti-Patterns for RAG

- Notes that only make sense when read top-to-bottom
- Heavy reliance on context from other notes (broken when retrieved in isolation)
- Unnamed code blocks without surrounding explanation
- Tables without headers or context sentences

### Metadata for Retrieval

```yaml
---
tags: [mlops, docker, ci-cd]      # Filtering
aliases: [DLC, Docker build cache] # Alternative search terms
rag_ready: true                    # Marks notes validated for ingestion
domain: mlops                      # Domain scoping for focused retrieval
---
```

---

## 5. Semantic Naming Conventions

### File Naming Rules

| Rule | Example | Rationale |
|---|---|---|
| Lowercase kebab-case | `model-drift-monitoring.md` | URL-safe, consistent |
| Noun-phrase or concept name | `feature-store-patterns.md` | Describes what it IS, not what it DOES |
| No version numbers | `mlflow-model-registry.md` (not `mlflow-v2-registry`) | Evergreen notes evolve in-place |
| No dates in filenames | Dates go in frontmatter | Filenames are semantic, not temporal |
| Specific over generic | `docker-layer-caching.md` (not `docker.md`) | Atomic concepts, not encyclopedic entries |

### Folder Naming Rules

| Rule | Example |
|---|---|
| Numbered prefix for top-level | `07-mlops/` |
| Descriptive subfolder names | `evergreen/`, `playbooks/`, `debugging/` |
| No nested numbering | `07-mlops/evergreen/` (not `07-mlops/01-evergreen/`) |

### Tag Naming Rules

| Rule | Example |
|---|---|
| Lowercase kebab-case | `#ci-cd`, `#model-drift` |
| Domain-scoped when needed | `#mlops`, `#aws`, `#databricks` |
| No abbreviations unless universal | `#ci-cd` (yes), `#k8s` (acceptable), `#dlc` (no — use `#docker`) |
| Prefer established terms | `#observability` (not `#monitoring-stuff`) |

---

## 6. Note Atomicity Best Practices

### The Atomic Note Principle

Each note should contain **one concept** that can be:
- Understood independently
- Linked to from multiple contexts
- Retrieved as a standalone chunk
- Updated without cascading changes

### Atomicity Checklist

- [ ] Can you summarize this note in one sentence?
- [ ] Would splitting it into two notes make each one clearer?
- [ ] Does it answer one specific question, not three?
- [ ] Could someone find and use this note without reading related notes first?
- [ ] Does the title accurately describe the full scope of the content?

### When to Split

Split a note when:
- It has two H2 sections that could each be their own note
- You find yourself linking to "the second half of X note"
- Different audiences would want different parts
- The note exceeds ~800 words of core content (excluding examples and metadata)

### When NOT to Split

Keep together when:
- Concepts are meaningless without each other (e.g., online/offline store within feature-store-patterns)
- Splitting would create notes too small to be useful
- The relationship IS the concept (e.g., training-serving skew requires both contexts)

---

## 7. GitHub-Compatible Documentation Structure

### Public Portfolio Layer

Portions of this vault can become public documentation. Structure for dual use:

```
quantpath-llm-wiki/
├── README.md                    ← Public: vault overview and navigation
├── 07-mlops/
│   ├── README.md                ← Public: MLOps layer introduction
│   ├── evergreen/
│   │   ├── README.md            ← Public: note index with descriptions
│   │   ├── mlflow-model-registry.md    ← Public: portfolio artifact
│   │   └── ...
│   ├── architecture/            ← Public: design documentation
│   ├── playbooks/               ← Private: operational procedures
│   └── debugging/               ← Private: internal patterns
```

### GitHub Rendering Considerations

| Feature | Obsidian | GitHub | Compatibility |
|---|---|---|---|
| Wikilinks `[[note]]` | Rendered | Raw text | Add standard links in Sources section |
| YAML frontmatter | Hidden | Rendered as table | Keep frontmatter clean and informative |
| Mermaid diagrams | Plugin | Native support | Prefer Mermaid for portable diagrams |
| Tags `#tag` | Indexed | Raw text | Tags in frontmatter (YAML array) for both |
| Callouts `> [!note]` | Rendered | Blockquote | Acceptable degradation |

### README.md Pattern for Public Folders

```markdown
# MLOps Knowledge Layer

Production-oriented evergreen notes on ML infrastructure, operations, and governance.

## Notes in This Section

| Note | Domain | Summary |
|---|---|---|
| [MLflow Model Registry](evergreen/mlflow-model-registry.md) | Model Management | Versioning and governance for ML models |
| [Docker Layer Caching](evergreen/docker-layer-caching.md) | Infrastructure | Build optimization for ML containers |
| ... | ... | ... |

## Architecture

This knowledge layer emphasizes systems thinking, failure modes, and operational readiness
over tutorial-style documentation.

## Related

- [AI/ML Foundations](../02-ai-ml/)
- [AWS Cloud](../04-aws-cloud/)
- [Databricks](../06-databricks-labs/)
```

### Visibility Levels

Use frontmatter `visibility` field to control what becomes public:

| Level | Meaning | Action |
|---|---|---|
| `PORTFOLIO_SAFE` | Can be published as-is | Include in public docs |
| `INTERNAL` | Contains personal learning context | Exclude from public |
| `DRAFT` | Incomplete, not yet validated | Exclude until promoted |

---

## 8. Maintenance Cadence

### Weekly
- Review new learning for note-worthy concepts
- Update existing notes with new connections
- Check that new notes have proper frontmatter and links

### Monthly
- Review MOC for completeness
- Identify gaps in knowledge graph
- Promote DRAFT notes to PORTFOLIO_SAFE where ready
- Archive stale or superseded notes

### Quarterly
- Validate RAG-readiness of all `rag_ready: true` notes
- Review tag taxonomy for consistency
- Update roadmap and planned notes
- Consider public documentation refresh

---

## Related Notes

- [[moc-mlops]] — MLOps knowledge map (hub)
- [[dashboard]] — vault-level command center
- [[quantpath-roadmap]] — overall learning roadmap
