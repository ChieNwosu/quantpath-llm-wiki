# RAG Readiness Guidelines — QuantPath LLM Wiki

**Purpose**: Standards for writing notes that will eventually be ingested into an Amazon Bedrock Knowledge Base.
**Last updated**: 2025-07-10

---

## What RAG Readiness Means

A RAG-ready note is one that can be chunked, embedded, and retrieved accurately by a vector search system. The goal is not to optimize for a specific embedding model — it is to write notes that are clear, self-contained, and factually grounded.

---

## Writing Standards for RAG-Ready Notes

### 1. Self-Contained
Each note should be understandable without reading other notes. Wikilinks are for human navigation; the RAG system sees each chunk independently.

**Good**: "Amortization is the process of paying off a loan through scheduled payments where the proportion of principal and interest shifts over time."
**Avoid**: "As described in the previous note, amortization works by..."

### 2. Concise and Chunked
- Use H2 and H3 headings to create natural chunk boundaries
- Keep sections to 100–300 words where possible
- Avoid long unbroken paragraphs
- Prefer bullet points over prose for lists of facts

### 3. Factually Grounded
- Cite sources: `(source: filename)` or `(source: AWS documentation)`
- Flag unverified claims: `[needs verification]`
- Do not present AI-generated content as verified fact without review

### 4. No Sensitive Content
Before a note is RAG-ready, verify:
- No `PRIVATE_ONLY` content
- No `SOURCE_LOCKED` verbatim text
- No API keys, credentials, or personal information
- No copyrighted course content

### 5. Structured Metadata
Include at the top of each note:
```markdown
**Summary**: One or two sentences.
**Type**: Atomic / Molecule / Entity / Project
**Sources**: (source: filename)
**Last updated**: YYYY-MM-DD
**Visibility**: PORTFOLIO_SAFE / PUBLIC_READY
```

---

## What to Include in RAG Ingestion

| Include | Exclude |
|---|---|
| `02-ai-ml/` concept notes | `PRIVATE_ONLY` notes |
| `03-data-sql/` concept notes | `SOURCE_LOCKED` notes |
| `04-aws-cloud/` service notes | `_system/` folder |
| `05-quant-finance/` concept notes | `_templates/` folder |
| `06-databricks-labs/` concept notes | `.kiro/` folder |
| `07-duke-coursera-wiki/` (PORTFOLIO_SAFE only) | `00-command-center/` operational notes |
| `08-projects/` project notes (not PM artifacts) | `10-sources/00-inbox/` raw sources |
| `09-entities/` entity notes | `Clippings/` |
| `01-maps-of-content/` MOCs (as navigation context) | PM artifacts marked PRIVATE_ONLY |

---

## Current RAG Readiness Status

| Folder | RAG Ready? | Notes |
|---|---|---|
| `02-ai-ml/` | ❌ Not yet | Most notes are empty stubs |
| `03-data-sql/` | ❌ Not yet | Most notes are empty stubs |
| `04-aws-cloud/` | 🔄 Partial | Certification notes ready; service stubs need content |
| `05-quant-finance/` | 🔄 Partial | Mortgage analytics notes ready; others are stubs |
| `06-databricks-labs/` | ❌ Not yet | Most notes are empty stubs |
| `08-projects/mortgage-rate-intelligence/` | ✅ Ready | Well-structured, source-cited, no private content |

---

## Future Bedrock Deployment

Target: Amazon Bedrock Knowledge Base
- S3 bucket as data source
- Bedrock Knowledge Base with chunking strategy
- Claude or Titan embeddings
- Query via Bedrock Agents or direct API

See `08-projects/project-llm-wiki-bedrock-rag.md` for the project note (when populated).
