# Obsidian to GitHub Workflow

**Purpose**: How to keep the Obsidian vault and GitHub repository in sync.
**Last updated**: 2025-07-10

---

## Overview

This vault lives locally in Obsidian and is version-controlled with Git. The GitHub remote is `quantpath-llm-wiki`. Changes flow:

```
Obsidian (local edit) → Git commit → GitHub push → Kiro Web access
```

---

## Daily Workflow

1. Edit notes in Obsidian as normal
2. When a meaningful set of changes is ready, commit via Git
3. Push to GitHub
4. Kiro Web can then read the latest version from GitHub

There is no auto-sync. Commits are intentional.

---

## What to Commit

**Always commit:**
- New permanent notes (atomic, molecule, entity, project)
- Updated MOCs
- New templates
- System log updates (`_system/log.md`)
- New steering files (`.kiro/steering/`)
- README and meta updates

**Never commit** (covered by `.gitignore`):
- `PRIVATE_ONLY` notes
- `SOURCE_LOCKED` clippings
- Raw source inbox (`10-sources/00-inbox/`)
- `.obsidian/workspace.json`
- Binary files (Excel, PDF, images)

---

## Commit Message Convention

Use short, descriptive commit messages:

```
add: amortization and refinance-break-even concept notes
update: moc-quant-finance with mortgage analytics links
fix: remove stale 12-reflections references from AGENTS.md
meta: add .gitignore and README for GitHub migration
```

Prefixes: `add:`, `update:`, `fix:`, `meta:`, `system:`, `remove:`

---

## Initial Setup Commands

### Option A — GitHub CLI

```bash
# 1. Navigate to vault folder
cd "C:\Users\chenw\OneDrive\Documents\llm-wiki"

# 2. Initialize git (if not already done)
git init

# 3. Review what will be staged (check .gitignore is working)
git status

# 4. Stage all safe files
git add .

# 5. Review staged files one more time
git status

# 6. Initial commit
git commit -m "meta: initial commit — QuantPath LLM Wiki vault"

# 7. Create GitHub repo (private) via GitHub CLI
gh repo create quantpath-llm-wiki --private --source=. --remote=origin --push

# 8. Verify
gh repo view quantpath-llm-wiki
```

### Option B — GitHub Desktop

1. Open GitHub Desktop
2. File → Add Local Repository → select `C:\Users\chenw\OneDrive\Documents\llm-wiki`
3. If prompted to initialize, click "Initialize Repository"
4. Review the changed files list — verify `.gitignore` is excluding private files
5. Write commit summary: `Initial commit — QuantPath LLM Wiki vault`
6. Click "Commit to main"
7. Click "Publish repository"
8. Set name: `quantpath-llm-wiki`
9. Set visibility: **Private**
10. Click "Publish Repository"

---

## Connecting to Kiro Web

After the repo is on GitHub:

1. Open Kiro Web
2. Connect your GitHub account if not already connected
3. Select the `quantpath-llm-wiki` repository
4. Kiro Web will have read/write access to all committed files
5. Kiro Web will respect `.gitignore` — excluded files are not visible

---

## Ongoing Sync Cadence

Suggested commit frequency:
- After each significant wiki-building session (ingestion, new notes, MOC updates)
- After each Kiro operation that creates or modifies notes
- Before switching between Obsidian and Kiro Web to avoid conflicts

---

## Conflict Prevention

- Do not edit the same note in both Obsidian and Kiro Web simultaneously
- Commit and push from Obsidian before switching to Kiro Web
- Pull latest changes in Obsidian before editing after a Kiro Web session:

```bash
git pull origin main
```
