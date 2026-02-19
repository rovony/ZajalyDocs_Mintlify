---
title: Folder Structure + Git + Cursor — Complete Guide
type: guide
status: published
owner: Malek
tags: [setup, git, cursor, vscode, folder-structure]
project: general
version: 1.0
created: 2026-02-19
updated: 2026-02-19
publish: false
---

# Folder Structure + Git + Cursor — Complete Guide

> Six root folders. Zaj prefix = your work. Underscore prefix = system. One Git repo, one Obsidian vault.

---

## Folder Structure

The repo lives at `C:\Zajaly\ZajalyDocs`. Obsidian opens the **entire root** as its vault. Six top-level folders — three Zaj-prefixed (your master content) and three underscore-prefixed (system/support, hidden in Obsidian):

```
ZajalyDocs/                          ← Git repo root + Obsidian vault root
├── _Admin/                          # System config, tools, internal assets
│   ├── Apps/                        # Utility scripts & integrations
│   │   ├── notion-sync/             # Make.com scenario configs
│   │   ├── inbox-processor/         # _Inbox processing scripts
│   │   └── Skillplate/              # Skillplate integration notes
│   ├── Business/                    # Contract templates, brand assets, ops
│   │   ├── Legal/                   # Terms, privacy, contracts
│   │   ├── Brand/                   # Logos, colors, style guide
│   │   └── Operations/              # SOPs, billing, onboarding
│   ├── Setup/                       # These setup guides (00-10)
│   ├── Scripts/                     # Automation scripts
│   └── Config/                      # Tool configs, API keys reference
├── _Inbox/                          # Universal capture zone — process weekly
├── _Sources/                        # Raw external reference material
│   ├── Servers/                     # Server-related source docs
│   ├── Laravel/                     # Laravel source docs
│   ├── SimpleBackups/               # SimpleBackups docs
│   └── [any tool or topic]/
├── ZajContent/                      # Publishing outputs
│   ├── Blog/                        # Posts → Hashnode (blog.zajaly.dev)
│   │   ├── Drafts/
│   │   └── Published/
│   └── Courses/                     # Skillplate scripts (EN / ES / AR)
│       ├── EN/
│       ├── ES/
│       └── AR/
├── ZajDocs/                         # Guides, tools, knowledge
│   ├── Guides/                      # Final how-tos by tech topic
│   │   ├── Servers/
│   │   ├── Laravel/
│   │   ├── React/
│   │   ├── Python/
│   │   ├── Databases/
│   │   ├── Git-DevOps/
│   │   ├── APIs/
│   │   ├── AI-ML/
│   │   └── Security/
│   ├── Tools/                       # Reviews, comparisons, current stack
│   ├── Defaults/                  # Snippets, cheatsheets, templates
│   │   ├── Templates/               # Obsidian Templater templates
│   │   ├── Cheatsheets/
│   │   ├── Snippets/
│   │   └── AI-Prompts/
│   └── _Archive/                    # Outdated content, kept for reference
└── ZajProjects/                     # SaaS product docs (1 per product)
    ├── Custojo/
    ├── Waraq/
    ├── LMS/
    ├── ResiBoard/
    ├── RepoMemo/
    └── DeployVault/
```

---

## Naming Convention

| Prefix | Folders | Purpose | In Obsidian? | On GitBook? |
|---|---|---|---|---|
| `Zaj` | ZajDocs, ZajContent, ZajProjects | Master content — your work | ✅ Visible | ZajDocs + ZajProjects yes |
| `_` | _Admin, _Inbox, _Sources | System/support | ❌ Hidden | ❌ Never |

**Why Zaj prefix?** In Obsidian, VS Code, or any file manager, you instantly know these are your master folders — not generic names that could be from any project.

**Why underscore prefix?** Sorts first alphabetically (keeps them grouped) but hidden from Obsidian's sidebar, keeping your workspace clean. Still accessible via Quick Switcher (Ctrl+O).

---

## Where Files Live

**One primary folder per file. Tags handle cross-referencing.**

| Content Type | Folder | Example |
|---|---|---|
| Server setup guide | `ZajDocs/Guides/Servers/` | `vps-initial-setup.md` |
| Tool review | `ZajDocs/Tools/` | `simplebackups-review.md` |
| Cheatsheet | `ZajDocs/Defaults/Cheatsheets/` | `git-cheatsheet.md` |
| Template | `ZajDocs/Defaults/Templates/` | `Guide-Template.md` |
| Custojo API docs | `ZajProjects/Custojo/` | `api-reference.md` |
| Blog post draft | `ZajContent/Blog/Drafts/` | `laravel-deployment-tips.md` |
| Course lesson | `ZajContent/Courses/EN/Server-Setup-101/` | `01-VPS-Basics.md` |
| Raw source material | `_Sources/SimpleBackups/` | `official-docs-notes.md` |
| Setup guide (this file) | `_Admin/Setup/` | `01-Folder-Structure-Git-Cursor.md` |
| Quick capture | `_Inbox/` | `idea-new-tool-comparison.md` |

**Cross-topic rule:** A SimpleBackups review lives in `ZajDocs/Tools/` with tags `[tools, backups, SimpleBackups]`. A SimpleBackups deployment guide lives in `ZajDocs/Guides/Servers/` with tags `[servers, backups, SimpleBackups]`. Dataview query `tags:SimpleBackups` finds both.

---

## Frontmatter Standard

Every file gets this YAML frontmatter:

```yaml
---
title: [Title]
type: guide | sop | reference | cheatsheet | review | comparison | course | blog
status: draft | review | published | outdated | archived
owner: Malek
tags: [topic, subtopic, tool-name]
tool: [tool name if applicable]
project: general | custojo | waraq | lms | resiboard | repomemo | deployvault
version: 1.0
created: YYYY-MM-DD
updated: YYYY-MM-DD
publish: true | false
---
```

**Key fields:**
- `type` — drives Dataview queries and template selection
- `status` — tracks lifecycle (draft → review → published → outdated → archived)
- `project` — links file to a product
- `publish` — gates Obsidian Publish (only `true` files are candidates)
- `tags` — enables cross-folder discovery via Dataview

---

## Git Setup

### Initialize the Repo

```powershell
cd "C:\Zajaly\ZajalyDocs"
git init
git remote add origin https://github.com/rovony/ZajalyDocs.git
git add .
git commit -m "Initial vault setup"
git branch -M main
git push -u origin main
```

### .gitignore

Create at vault root (`C:\Zajaly\ZajalyDocs\.gitignore`):

```gitignore
# Obsidian workspace (device-specific)
.obsidian/workspace.json
.obsidian/workspace-mobile.json
.obsidian/cache/

# OS files
.DS_Store
Thumbs.db
desktop.ini

# Obsidian trash
.trash/

# Node
node_modules/

# Temp files
*.tmp
*.swp
*~

# Secrets
.env
*.key
```

**What IS tracked by Git:**
- All markdown files in all folders
- `.obsidian/plugins/` — plugin configs (so plugins are consistent)
- `.obsidian/themes/` — theme files
- `.obsidian/snippets/` — custom CSS
- `.obsidian/app.json` — core settings including excluded files
- `_Admin/`, `_Inbox/`, `_Sources/` — hidden in Obsidian but tracked in Git

### Branch Strategy

**Keep it simple:** work on `main` only. This is a documentation vault, not application code.

If you want to experiment with big restructures:
```powershell
git checkout -b restructure-guides
# Make changes, test in Obsidian
git checkout main
git merge restructure-guides
git branch -d restructure-guides
```

---

## Cursor / VS Code Setup

### Open the Vault

Open `C:\Zajaly\ZajalyDocs` in Cursor or VS Code. Same folder as Obsidian — two editors for different purposes:
- **Obsidian** — writing, linking, publishing, mobile
- **Cursor/VS Code** — bulk edits, AI assistance, Git operations, code-heavy docs

### .cursorrules

Create at vault root for Cursor AI context:

```
# ZajalyDocs Vault Rules

## About
This is a documentation vault for Zajaly LLC's SaaS products. It contains guides, SOPs, tool reviews, project docs, blog drafts, and course scripts.

## Structure
- ZajDocs/ → Guides, tools, essentials (published to GitBook + Obsidian Publish)
- ZajProjects/ → Per-product documentation (published to GitBook)
- ZajContent/ → Blog posts and course scripts (published to Hashnode/Skillplate)
- _Admin/ → System config, setup guides (never published)
- _Inbox/ → Raw captures (never published)
- _Sources/ → External reference material (never published)

## Rules for creating docs
1. Always include YAML frontmatter with: title, type, status, owner, tags, project, version, created, updated, publish
2. Use wikilinks for internal references: [[filename]] or [[folder/filename|Display Text]]
3. Heading hierarchy: # for title, ## for sections, ### for subsections
4. Code blocks: always specify language (```bash, ```php, ```javascript, etc.)
5. Status values: draft, review, published, outdated, archived
6. Tags: lowercase, hyphenated (e.g., server-setup, laravel-deployment)
7. One topic per file. Cross-reference with tags and wikilinks.
```

### Recommended Extensions

| Extension | Purpose |
|---|---|
| **Markdown All in One** | Preview, TOC auto-generation, shortcuts |
| **Markdown Preview Enhanced** | Better rendering |
| **markdownlint** | Catch formatting issues |
| **Foam** | Wikilink support, graph view in VS Code |
| **Git Graph** | Visual git history |
| **YAML** | Frontmatter syntax validation |
| **Better TOML** | Config file support |

### Keyboard Shortcuts (Cursor/VS Code)

| Action | Shortcut |
|---|---|
| Open file by name | `Ctrl+P` |
| Search across vault | `Ctrl+Shift+F` |
| Toggle sidebar | `Ctrl+B` |
| Open terminal | `` Ctrl+` `` |
| Git: stage all | `Ctrl+Shift+G` then `+` |
| Markdown preview | `Ctrl+Shift+V` |

---

## Workflow: How Obsidian + Cursor + Git Work Together

```
1. Write in Obsidian (markdown + wikilinks + templates)
       ↓
2. Obsidian Git plugin auto-commits every 30 min
       ↓
3. Push to GitHub (rovony/ZajalyDocs)
       ↓
4. GitBook auto-syncs from GitHub (ZajDocs/ + ZajProjects/)
       ↓
5. Obsidian Sync mirrors to phone/tablet in real-time
       ↓
6. Cursor for bulk edits, refactoring, AI-assisted writing
       ↓
7. Manual commit + push from Cursor when done
```

All three tools (Obsidian, Cursor, Git) operate on the same folder. No file duplication. No sync conflicts between them because:
- **Obsidian Git** handles periodic auto-commits
- **Obsidian Sync** handles real-time device sync (different layer than Git)
- **Cursor** saves files to disk → Obsidian sees changes immediately

---

## Creating New Folders

When adding a new product or guide topic:

```powershell
# New product
mkdir "C:\Zajaly\ZajalyDocs\ZajProjects\NewProduct"

# New guide topic
mkdir "C:\Zajaly\ZajalyDocs\ZajDocs\Guides\NewTopic"
```

Always create a `README.md` inside new folders (used by GitBook as section home page and by Folder Note plugin in Obsidian).

---

## Checklist

- [ ] Folder structure created at `C:\Zajaly\ZajalyDocs` with all 6 root folders
- [ ] Git initialized and pushed to `github.com/rovony/ZajalyDocs`
- [ ] `.gitignore` in place
- [ ] `.cursorrules` in place
- [ ] Cursor/VS Code opens the vault with recommended extensions
- [ ] Obsidian opens the same folder as vault
- [ ] Test: create a file in Cursor → see it in Obsidian immediately

---

*Related: [[02-Obsidian-Setup]] | [[03-GitBook-Free-Setup]]*
*Save to: C:\Zajaly\ZajalyDocs\_Admin\Setup\01-Folder-Structure-Git-Cursor.md*
*Version: 1.0 — February 19, 2026*
