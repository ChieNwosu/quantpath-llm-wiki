---
inclusion: always
---

# Folder Expansion Policy — QuantPath LLM Wiki

## Default Rule

**Do not create new folders without justification.** The existing 14-folder structure covers all current domains. Conservative folder creation keeps the vault navigable and the Obsidian graph clean.

## When a New Subfolder Is Justified

A subfolder within an existing folder may be created when ALL of the following are true:

1. There are **5 or more notes** that clearly belong together under a shared sub-topic.
2. The grouping adds **navigational value** — it would be genuinely confusing to browse without the subfolder.
3. The sub-topic is **stable** — not a temporary project phase or a one-time source batch.
4. The subfolder **does not duplicate** an existing folder's purpose.

## Pre-Approved Subfolders

These subfolders are already approved and may be created without asking:

```
10-sources/00-inbox/
10-sources/00-inbox/notebooklm-exports/
10-sources/00-inbox/web-clips/
10-sources/00-inbox/coursera-notes/
10-sources/source-summaries/
10-sources/source-registry/
```

## Subfolders That May Be Created With Explanation

These are likely future needs. Create them when the note count justifies it, and explain why:

| Potential Subfolder | Trigger Condition |
|---|---|
| `07-duke-coursera-wiki/duke-r-programming/` | 5+ R programming course notes |
| `07-duke-coursera-wiki/duke-statistics/` | 5+ statistics course notes |
| `07-duke-coursera-wiki/duke-defi/` | 5+ DeFi course notes |
| `07-duke-coursera-wiki/duke-finance/` | 5+ finance course notes |
| `02-ai-ml/agentic-ai/` | 5+ agentic AI notes (MCP, Strands, Bedrock Agents) |
| `04-aws-cloud/bedrock/` | 5+ Bedrock-specific notes |

## New Top-Level Folders

**Never create a new top-level folder without explicit user approval.**

If you believe a new top-level folder is needed, report the recommendation with:
- The proposed folder name and number prefix
- The notes that would move into it
- Why the existing structure cannot accommodate them

## Folder Naming Convention

- Lowercase with hyphens: `my-new-folder/`
- Numbered prefixes for top-level folders: `13-new-domain/`
- No spaces, no underscores, no camelCase

## What to Do Instead of Creating Folders

Before creating a subfolder, consider:
- Can a MOC note in `01-maps-of-content/` serve the same navigational purpose?
- Can a `## Section` heading within an existing MOC group these notes?
- Can wikilinks between notes create the needed structure without a folder?

Often, a well-maintained MOC is better than a new folder.
