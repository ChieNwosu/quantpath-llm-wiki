---
inclusion: always
---

# Note Formatting Rules — QuantPath LLM Wiki

## Filename Convention

- All filenames: **lowercase with hyphens**, no spaces, no underscores, no camelCase.
- Examples: `rag.md`, `sharpe-ratio.md`, `project-cfpb-dashboard.md`
- Exception: system files like `AGENTS.md` and `CLAUDE.md` use uppercase by convention.

## Required Fields

Every permanent note should include near the top:

```markdown
**Summary**: One or two sentences.
**Type**: Atomic / Molecule / Entity / Project / MOC / Source Summary / Course Note
**Sources**: [[source-note]] or (source: filename) or external reference
**Last updated**: YYYY-MM-DD
```

## Wikilinks

- Use `[[note-name]]` for all internal links. Never use relative file paths.
- Link to related concept notes, MOC notes, entity notes, and project notes where relevant.
- Do not over-link. Link when the connection adds navigational or conceptual value.

## Visibility Labels

Every note should carry one visibility label (in the header or as a callout):

| Label | Meaning |
|---|---|
| `PRIVATE_ONLY` | Personal reflections, career strategy, private plans |
| `PORTFOLIO_SAFE` | Can be adapted for GitHub, LinkedIn, README, interviews |
| `SOURCE_LOCKED` | Based on paid/copyrighted material; summarize only, do not publish |
| `PUBLIC_READY` | Reviewed, source-safe, privacy-safe, ready for GitHub or LinkedIn |

## Note Type Formats

### Atomic / Concept Note
```markdown
# Concept Name

**Summary**:
**Type**: Atomic note
**Sources**:
**Last updated**:

## Core Idea

## Why It Matters

## Example

## Related Notes
- [[related-note]]

## Portfolio Connection
```

### Molecule Note
```markdown
# Topic or Workflow Name

**Summary**:
**Type**: Molecule note
**Combines**: [[atomic-one]], [[atomic-two]]
**Sources**:
**Last updated**:

## Explanation

## Workflow or Architecture

## Example

## Project Connection

## Related Notes
```

### Entity Note
```markdown
# Entity Name

**Entity type**: Person / Company / Tool / Course / Dataset / Institution
**Summary**:
**Last updated**:

## What This Is

## Why It Matters to My Learning Path

## Related Notes
- [[related-note]]

## Sources
```

### Project Note
```markdown
# Project: Project Name

**Status**: Idea / Planning / Building / Documenting / Published
**Domain**:
**Tools**:
**GitHub repo**:
**Public export status**: Private / Portfolio-safe / Published

## Business or Research Question

## Technical Workflow

## Dataset or Source

## Skills Demonstrated

## GitHub Documentation Plan

## Interview Story

## Related Notes
```

### Source Summary Note
```markdown
# Source: Title

**Source type**: Course / Book / Documentation / Dataset / Video / AI Output / Personal Note
**Original file or link**:
**Date added**:
**Status**: Unprocessed / Partially Integrated / Integrated / Needs Review

## Summary

## Key Ideas

## Potential Wiki Pages to Create

## Portfolio or Project Connections

## Verification Notes
```

## Style Rules

- Write in clear, plain language. Short paragraphs.
- Use examples whenever possible.
- Use markdown headings consistently (H1 for title, H2 for sections, H3 for subsections).
- Avoid long AI-generated prose dumps. Compress for future review.
- Mark uncertainty explicitly: `[needs verification]`
- Separate facts from interpretation using `## Verified Facts` and `## My Interpretation` sections when relevant.
- Source conflicts: `Source conflict: Source A says X, while Source B says Y.`

## Citation Style

Inside notes, cite sources like this:
```
(source: filename-or-source-note)
```

For external sources:
```
(source: "Book Title" by Author, Chapter X)
(source: AWS documentation, service name)
```
