---
title: Notion Sync — Complete Setup Guide
type: guide
status: published
owner: Malek
tags: [setup, notion, sync, make, automation]
project: general
version: 1.0
created: 2026-02-19
updated: 2026-02-19
publish: false
---

# Notion Sync — Complete Setup Guide

> No native sync exists between Obsidian and Notion. Best available: Make.com automation (free tier, 1,000 ops/mo).

---

## The Honest Truth

No tool in our stack has native bidirectional Notion sync. Notion's API is write-friendly but export-unfriendly. Here's what actually works, what doesn't, and the recommended setup.

---

## Recommended: Make.com Automation (Free Tier)

Make.com (formerly Integromat) connects Notion ↔ GitHub with visual automation. Free tier = 1,000 operations/month — enough for a few syncs per day.

### Architecture

```
Notion (write/collaborate)
    ↓ Make.com scenario (every 15 min)
GitHub repo: rovony/ZajalyDocs (source of truth)
    ↓ automatic (Git push triggers)
Obsidian (local vault via Git plugin auto-pull)
    AND
GitBook (published docs via Git sync)
    AND
Mintlify (dev docs via Git sync — separate repo)
```

---

## Step 1 — Create a Notion Integration

1. Go to **https://www.notion.so/my-integrations**
2. Click **+ New integration**
3. Name: `ZajalyDocs Sync`
4. Associated workspace: your Notion workspace
5. Capabilities: **Read content**, **Update content**, **Insert content**
6. Click **Submit** → copy the **Internal Integration Secret** (starts with `ntn_`)
7. Save this token securely — you'll need it for Make.com

### Connect Integration to Your Database

1. In Notion, open the database you want to sync (e.g., a "Documentation" database)
2. Click **...** (three dots menu) → **Connections** → **Connect to** → search `ZajalyDocs Sync`
3. Click **Confirm**

Without this step, the integration has zero access to your pages.

---

## Step 2 — Set Up Your Notion Database

Create a Notion database for documentation if you don't already have one:

**Database properties:**

| Property | Type | Maps to (in Obsidian) |
|---|---|---|
| Title | Title | `title` in frontmatter |
| Status | Select (Draft, Review, Published) | `status` in frontmatter |
| Type | Select (guide, sop, review, etc.) | `type` in frontmatter |
| Tags | Multi-select | `tags` in frontmatter |
| Project | Select (general, custojo, waraq, etc.) | `project` in frontmatter |
| Target Folder | Select (ZajDocs/Guides, ZajProjects/Custojo, etc.) | File path in Git |
| Last Synced | Date | Tracks sync timestamp |

The `Target Folder` property tells Make.com where to place the file in your Git repo.

---

## Step 3 — Create Make.com Account

1. Go to **https://make.com** → Sign up (free)
2. Free tier: **1,000 operations/month**, 2 active scenarios
3. Operations reset monthly

---

## Step 4 — Scenario 1: Notion → GitHub (Notion as source)

This scenario watches for new or updated Notion pages and pushes them to your GitHub repo as markdown files.

### 4A — Create Scenario

1. Make.com → **Create a new scenario**
2. Name: `Notion → GitHub`

### 4B — Add Trigger: Watch Database Items

1. Add module: **Notion → Watch Database Items**
2. Connect your Notion account (paste the integration token)
3. Select your database
4. Watch: **Updated pages** (catches both new and edited)
5. Schedule: **Every 15 minutes**

### 4C — Add Transform: Format as Markdown

1. Add module: **Tools → Text Aggregator** (or **Set Variable**)
2. Build the markdown content:

```
---
title: {{Title}}
type: {{Type}}
status: {{Status}}
tags: [{{Tags}}]
project: {{Project}}
publish: false
synced_from: notion
---

# {{Title}}

{{Page Content}}
```

> [!NOTE]
> Notion's API returns page content as blocks, not markdown. Make.com's Notion module can extract rich text, but complex formatting (tables, toggles, embedded databases) may not convert cleanly. For complex pages, use Make.com to create a stub file and finalize formatting in Obsidian.

### 4D — Add Action: Create or Update File in GitHub

1. Add module: **GitHub → Create or Update a File**
2. Connect your GitHub account
3. Repository: `rovony/ZajalyDocs`
4. Branch: `main`
5. File path: `{{Target Folder}}/{{Slugified Title}}.md`
6. File content: the markdown from step 4C
7. Commit message: `sync from notion: {{Title}}`

### 4E — Activate

Turn on the scenario. It runs every 15 minutes, checking for Notion changes.

---

## Step 5 — Scenario 2: GitHub → Notion (Obsidian/Git as source)

This scenario watches for Git pushes and updates Notion when you edit files in Obsidian or VS Code.

### 5A — Create Scenario

1. Make.com → **Create a new scenario**
2. Name: `GitHub → Notion`

### 5B — Add Trigger: Watch Repository Events

1. Add module: **GitHub → Watch Events** (or **Watch Push Events**)
2. Repository: `rovony/ZajalyDocs`
3. Events: **Push**

### 5C — Add Filter

Only process files in synced folders (don't sync `_Admin/`, `.obsidian/`, etc.):
- Condition: file path **starts with** `ZajDocs/` OR `ZajProjects/`
- AND file extension **equals** `.md`

### 5D — Add Action: Update Notion Page

1. Add module: **Notion → Update a Database Item** (or **Create a Database Item**)
2. Match by: Title property (find existing page by filename)
3. Update: page content, status, last synced date
4. If no match found: create new page

### 5E — Activate

Turn on the scenario. Now edits in Obsidian → Git push → Make.com → Notion.

---

## Step 6 — How It Flows End-to-End

```
You edit in Notion
    → Make Scenario 1 runs (every 15 min)
    → Commits markdown to GitHub
    → Obsidian Git plugin auto-pulls (every 30 min)
    → File appears in your vault
    → GitBook Git sync picks it up (~1 min)
    → Published on GitBook

You edit in Obsidian
    → Obsidian Git auto-commits + pushes (every 30 min)
    → Make Scenario 2 runs (triggered by push)
    → Updates Notion page
    → Collaborators see changes in Notion
```

**Worst-case latency:** ~45 min for a round trip (Notion → GitHub → Obsidian). Typical: 15-30 min.

---

## Alternative: obsidianotion Plugin (One-Way)

If you just need to pull Notion content into Obsidian once (migration, not ongoing sync):

1. In Obsidian: **Settings → Community plugins → Browse** → search `obsidianotion`
2. Install and enable
3. Configure:
   - Notion API key: paste your integration token
   - Database ID: from your Notion database URL
4. Run the import → pages download as markdown into your vault

**Best for:** One-time migration of existing Notion content. Not suitable for ongoing bidirectional sync.

---

## Alternative: Notion Export + Manual Import

For occasional bulk transfers:

1. Notion → **Settings** → **Export all workspace content** → Markdown & CSV
2. Unzip the export
3. Copy relevant markdown files to appropriate folders in `ZajalyDocs/`
4. Clean up Notion's export formatting (it adds UUIDs to filenames, uses inconsistent heading levels)

**Best for:** Initial migration before setting up automation.

---

## GitBook ↔ Notion

No native integration. The path goes through GitHub:

```
Notion → Make.com → GitHub → GitBook (Git sync)
GitBook → GitHub (Git sync) → Make.com → Notion
```

Both directions are handled by the two Make.com scenarios above.

---

## Mintlify ↔ Notion

Mintlify is a separate repo (`rovony/zajaly-docs`), so you'd need a third Make.com scenario if you want Notion to sync there. On free tier (2 scenarios max), this isn't possible.

**Recommendation:** For Mintlify content, write in VS Code/Cursor directly in the Mintlify repo. Don't route through Notion.

---

## Free Tier Limits & Optimization

| Limit | Value |
|---|---|
| Operations/month | 1,000 |
| Active scenarios | 2 |
| Minimum interval | 15 minutes |
| Data transfer | 100 MB/month |

**How to stay within 1,000 ops:**
- Each scenario run that finds nothing = 1 operation
- Each page synced = ~3-5 operations (trigger + transform + action)
- At 15-min intervals, 2 scenarios = ~5,760 check operations/month (just triggers)
- Reduce to 30-min intervals if hitting limits

> [!TIP]
> Set scenarios to run every 30 minutes instead of 15 to halve operation usage. The delay is negligible for documentation sync.

---

## Troubleshooting

### Make.com can't access Notion database
**Fix:** Ensure the integration is connected to the specific database (not just the workspace). Click **...** on the database → **Connections** → add your integration.

### GitHub commits have wrong file paths
**Fix:** Check the `Target Folder` property in Notion. Make sure it matches your actual folder structure (`ZajDocs/Guides/Servers/`, not `Docs/Guides/Servers/`).

### Rich formatting lost in sync
**Expected.** Notion's toggles, embedded databases, columns, and synced blocks don't have markdown equivalents. Stick to headings, paragraphs, lists, code blocks, and images for content you plan to sync.

### Operations running out
**Fix:** Increase interval from 15 min to 30 or 60 min. Or upgrade Make.com ($9/mo for 10,000 ops).

---

## Checklist — Complete Notion Sync

- [ ] Notion integration created (`ZajalyDocs Sync`) with read/update/insert permissions
- [ ] Integration connected to target database(s) in Notion
- [ ] Notion database has correct properties (Title, Status, Type, Tags, Project, Target Folder)
- [ ] Make.com account created (free tier)
- [ ] Scenario 1: Notion → GitHub created and tested
- [ ] Scenario 2: GitHub → Notion created and tested
- [ ] Both scenarios activated and running on schedule
- [ ] End-to-end test: edit in Notion → verify appears in Obsidian vault
- [ ] End-to-end test: edit in Obsidian → push → verify appears in Notion

Setup time: ~2-3 hours. Cost: $0.

---

*Related: [[02-Obsidian-Setup]] | [[03-GitBook-Free-Setup]]*
*Save to: C:\Zajaly\ZajalyDocs\_Admin\Setup\06-Notion-Sync.md*
*Version: 1.0 — February 19, 2026*
