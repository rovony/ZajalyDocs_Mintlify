---
title: ZajalyDocs — Knowledge Hub
type: index
status: published
owner: Malek
created: 2026-02-18
updated: 2026-02-19
tags: [home, index]
---

# ZajalyDocs

> Zajaly's single source of truth for guides, SOPs, references, tools, and product documentation.

> [!NOTE]
> This is the **Obsidian vault** (`ZajDocs/` folder only). For the full root structure see the main [README](../../../README.md).

---

## Quick Navigation

### 📘 [Guides](Guides/) — Step-by-step knowledge
Everything organized by topic: Servers, Laravel, React, Python, Databases, Git/DevOps, APIs, AI/ML, Security.

### 📦 [Projects](Projects/) — Product knowledge
Docs, notes, and changelogs for each product: Custojo, Waraq, LMS, ResiBoard, RepoMemo, DeployVault.

### 🔧 [Tools](Tools/) — Tool research & setup
Reviews, comparisons, setup guides, and your current stack documentation.

### ⭐ [Defaults](Defaults/) — Your daily toolkit
Cheatsheets, snippets, AI prompts, templates, Cursor rules. Things you reach for constantly.

### 🗄️ [_Archive](_Archive/) — Deprecated and old content

---

## How This Works

- **Every file has frontmatter** — tags, status, type, project, and tool (when applicable)
- **One folder, many tags** — a file lives where you'd look first; tags handle cross-topic links
- **Dataview queries** — `type:guide AND tags:SimpleBackups` finds anything, anywhere
- **Publish selectively** — only files with `publish: true` go to Obsidian Publish
- **Git tracks everything** — auto-commits every 30 min to GitHub

---

## Standard Frontmatter

```yaml
---
title: [Title]
type: guide | sop | reference | cheatsheet | review | comparison
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

---

## Setup

See [_Admin/ZajalyDocs/Setup/00-MASTER-SETUP-GUIDE.md](../../../_Admin/ZajalyDocs/Setup/00-MASTER-SETUP-GUIDE.md) for complete setup instructions.
