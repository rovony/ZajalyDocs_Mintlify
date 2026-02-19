---
title: Action Plan — Complete Setup Checklist
type: guide
status: published
owner: Malek
tags: [setup, action-plan, checklist]
project: general
version: 1.0
created: 2026-02-19
updated: 2026-02-19
publish: false
---

# Action Plan — Complete Setup Checklist

> 3-week rollout. Week 1 = foundation. Week 2 = publishing. Week 3 = sync + courses. Total cost: $12/mo.

---

## Week 1 — Foundation (Do This First)

### Day 1-2: Folder Structure + Git

- [ ] Create `C:\Zajaly\ZajalyDocs\` with all 6 root folders:
  - `_Admin/` (with `Apps/`, `Business/`, `Setup/`, `Scripts/`, `Config/` subfolders)
  - `_Inbox/`
  - `_Sources/`
  - `ZajContent/` (with `Blog/Drafts/`, `Blog/Published/`, `Courses/EN/`, `Courses/ES/`, `Courses/AR/`)
  - `ZajDocs/` (with `Guides/`, `Tools/`, `Defaults/`, `_Archive/`)
  - `ZajProjects/` (with `Custojo/`, `Waraq/`, `LMS/`, `ResiBoard/`, `RepoMemo/`, `DeployVault/`)
- [ ] Create `.gitignore` at vault root (see [[01-Folder-Structure-Git-Cursor]])
- [ ] Create `.cursorrules` at vault root
- [ ] Initialize Git repo → push to `github.com/rovony/ZajalyDocs`
- [ ] Save all setup guides (00-10) to `_Admin/Setup/`

**Reference:** [[01-Folder-Structure-Git-Cursor]]

### Day 2-3: Obsidian Setup

- [ ] Download + install Obsidian from obsidian.md
- [ ] Open folder as vault → select `C:\Zajaly\ZajalyDocs` (ROOT, not a subfolder)
- [ ] Configure editor settings (source mode, line numbers, spellcheck, readable line length)
- [ ] Configure Files & Links (wikilinks ON, auto-update links, `_assets` attachment subfolder)
- [ ] Hide `_Admin`, `_Inbox`, `_Sources` from sidebar (Settings → Files & Links → Excluded files)
- [ ] Install Minimal theme + Style Settings plugin
- [ ] Install all community plugins:
  - File Hider → set `Ctrl+Shift+H` hotkey
  - Obsidian Git → auto-backup every 30 min
  - Dataview → enable JavaScript + inline queries
  - Templater → template folder: `ZajDocs/Defaults/Templates`
  - Calendar, Folder Note, Tag Wrangler, Linter, Iconize, Various Complements
- [ ] Set folder icons with Iconize: 📖 ZajDocs, ✏️ ZajContent, 🚀 ZajProjects
- [ ] Verify: sidebar shows only 3 Zaj folders
- [ ] Verify: Quick Switcher (Ctrl+O) finds files in hidden `_` folders

**Reference:** [[02-Obsidian-Setup]]

### Day 3-4: Obsidian Sync + Publish

- [ ] Purchase Obsidian Sync ($4/mo) at obsidian.md/pricing
- [ ] Create remote vault `ZajalyDocs` with encryption password
- [ ] Connect Sync → verify status shows "Connected"
- [ ] Exclude `workspace.json` and `workspace-mobile.json` from Sync
- [ ] Connect Sync on phone/tablet → verify same content appears
- [ ] Verify hidden folder settings transferred to mobile
- [ ] Purchase Obsidian Publish ($8/mo)
- [ ] Set custom domain: `vault.zajaly.dev`
- [ ] In Cloudflare: CNAME `vault` → `publish-main.obsidian.md` (DNS only, gray cloud)
- [ ] Verify domain → set password on published site
- [ ] Publish one test file → verify at `vault.zajaly.dev`
- [ ] Enable graph view, navigation, search, backlinks in Publish settings

**Reference:** [[02-Obsidian-Setup]]

### Day 4-5: Templates + First Content

- [ ] Create templates in `ZajDocs/Defaults/Templates/`:
  - Guide-Template.md
  - SOP-Template.md
  - Tool-Review-Template.md
  - Comparison-Template.md
  - Course-Lesson-Template.md
  - Blog-Post-Template.md
- [ ] Create `Dashboard.md` at vault root with Dataview queries
- [ ] Write first 3 guides using templates (pick your most needed topics)
- [ ] Verify: Obsidian Git committed and pushed to GitHub

---

## Week 2 — Publishing

### Day 6-7: GitBook

- [ ] Create `.gitbook.yaml` + `README.md` in `ZajDocs/`
- [ ] Create `.gitbook.yaml` + `README.md` in `ZajProjects/Custojo/`
- [ ] Create `.gitbook.yaml` + `README.md` in `ZajProjects/Waraq/`
- [ ] Create `SUMMARY.md` in each synced folder
- [ ] Commit and push all config files
- [ ] Create GitBook account at gitbook.com (sign up with GitHub)
- [ ] Create organization: `Zajaly`
- [ ] Create 3 spaces: ZajalyDocs, Custojo, Waraq
- [ ] Connect Git Sync for each space (monorepo paths):
  - ZajalyDocs → `ZajDocs`
  - Custojo → `ZajProjects/Custojo`
  - Waraq → `ZajProjects/Waraq`
- [ ] Sync direction: GitHub → GitBook (first sync)
- [ ] Create Docs Sites → set URL slugs: `/docs`, `/custojo`, `/waraq`
- [ ] Publish all 3 sites
- [ ] Set ZajalyDocs to **Unlisted**, Custojo + Waraq to **Public**
- [ ] Verify bidirectional sync: edit in VS Code → appears in GitBook, and vice versa

**Reference:** [[03-GitBook-Free-Setup]]

### Day 8-9: Mintlify

- [ ] Create Mintlify account at mintlify.com (GitHub sign-in)
- [ ] Create project → connect to repo `rovony/zajaly-docs` (SEPARATE from ZajalyDocs)
- [ ] Clone repo locally to `C:\Zajaly\Projects\mintlify-docs`
- [ ] Install Mintlify CLI: `npm install -g mint`
- [ ] Configure `docs.json` (navigation, colors, logo)
- [ ] Test locally: `mint dev` → verify at localhost:3000
- [ ] Custom domain: `docs.zajaly.dev` in Dashboard → Settings → Domain Setup
- [ ] Cloudflare: CNAME `docs` → `cname.mintlify-dns.com` (DNS only)
- [ ] Cloudflare: SSL → Full (strict), disable "Always Use HTTPS"
- [ ] Push → auto-deploy → verify at `docs.zajaly.dev`

**Reference:** [[04-Mintlify-Free-Setup]]

### Day 9-10: Hashnode + Featurebase

- [ ] Create Hashnode account → create publication `Zajaly Blog`
- [ ] Custom domain: `blog.zajaly.dev` → CNAME `blog` → `hashnode.network` (DNS only)
- [ ] Verify domain in Hashnode
- [ ] Enable GitHub backup integration
- [ ] Publish first test blog post
- [ ] Create Featurebase account → workspace: `Zajaly`
- [ ] Custom domain: `changelog.zajaly.dev` → CNAME as shown in Featurebase (DNS only)
- [ ] Verify domain
- [ ] Enable feedback board
- [ ] Publish first changelog entry

**Reference:** [[05-Publishing-Stack]]

### Day 10: DNS Verification

- [ ] Verify ALL Cloudflare CNAME records are set:

| Subdomain | CNAME Target | Status |
|---|---|---|
| `vault.zajaly.dev` | `publish-main.obsidian.md` | ☐ Verified |
| `docs.zajaly.dev` | `cname.mintlify-dns.com` | ☐ Verified |
| `blog.zajaly.dev` | `hashnode.network` | ☐ Verified |
| `changelog.zajaly.dev` | (Featurebase target) | ☐ Verified |
| `learn.zajaly.dev` | (Skillplate target) | ☐ Verified |

- [ ] All set to DNS only (gray cloud) — except where Cloudflare proxy is specifically required
- [ ] Mintlify: SSL set to Full (strict), "Always Use HTTPS" disabled

---

## Week 3 — Sync + Courses

### Day 11-12: Notion Sync

- [ ] Create Notion integration at notion.so/my-integrations
- [ ] Connect integration to target database(s) in Notion
- [ ] Set up Notion database with correct properties (Title, Status, Type, Tags, Project, Target Folder)
- [ ] Create Make.com account (free)
- [ ] Build Scenario 1: Notion → GitHub (watch database, format markdown, commit to repo)
- [ ] Build Scenario 2: GitHub → Notion (watch push events, update Notion pages)
- [ ] Test end-to-end: edit in Notion → appears in Obsidian vault
- [ ] Test end-to-end: edit in Obsidian → push → appears in Notion
- [ ] Activate both scenarios on schedule

**Reference:** [[06-Notion-Sync]]

### Day 12-13: Skillplate

- [ ] Activate Skillplate account with AppSumo license
- [ ] Configure Brand Kit (logo, colors, fonts)
- [ ] Connect Stripe (and/or PayPal)
- [ ] Custom domain: `learn.zajaly.dev` → CNAME as shown in Skillplate (DNS only)
- [ ] Verify domain
- [ ] Create first course using AI Course Builder
- [ ] Add at least one lesson (text or video)
- [ ] Set up landing page for the course
- [ ] Configure welcome email automation
- [ ] Create course folder structure in `ZajContent/Courses/EN/`

**Reference:** [[07-Skillplate-Courses]]

### Day 13-14: Video Generation (Optional)

- [ ] Create Synthesia account → test with free video (watermarked)
- [ ] Write a test lesson script in the Course-Lesson-Template
- [ ] Generate video from script → download MP4
- [ ] Upload to Skillplate lesson
- [ ] Evaluate quality — decide if Starter plan ($18/mo) is worth it

**Reference:** [[07-Skillplate-Courses]] Part C

---

## Month 2 — Optimize & Produce

### Evaluate

- [ ] Which publishing tools are you actually using weekly?
- [ ] Which tools feel redundant? (GitBook vs Mintlify overlap?)
- [ ] Is Notion sync providing value, or is it just complexity?
- [ ] Is video generation worth the Synthesia cost?

### Produce

- [ ] First complete Server/Setup guide series (3+ guides)
- [ ] First tool comparison (2+ tools)
- [ ] First published blog post on Hashnode
- [ ] First changelog entry on Featurebase
- [ ] First course published on Skillplate (at least 3 lessons)

### Maintain

- [ ] Weekly `_Inbox/` processing (move captures to permanent homes)
- [ ] Monthly status review (find `status:outdated`, update or archive)
- [ ] Monthly Sync/Publish review (check what's published, unpublish stale content)

---

## Monthly Cost Summary

| Tool | Cost | Purpose |
|---|---|---|
| Obsidian app | Free | Local editor |
| Obsidian Sync | $4/mo | Multi-device sync |
| Obsidian Publish | $8/mo | Published site + password + custom domain |
| GitHub | Free | Version control + backup |
| GitBook | Free | Product docs (`gitbook.io` subdomain) |
| Mintlify | Free | Dev docs (`docs.zajaly.dev`) |
| Featurebase | Free | Changelog + feedback (`changelog.zajaly.dev`) |
| Hashnode | Free | Blog (`blog.zajaly.dev`) |
| Skillplate | $0 (lifetime) | Courses (`learn.zajaly.dev`) |
| Make.com | Free | Notion sync (1,000 ops/mo) |
| **Total** | **$12/mo** | Complete documentation system |

**Optional later:**
- Synthesia Starter → $18/mo (AI video for courses)
- Make.com Pro → $9/mo (if 1,000 ops/mo isn't enough)
- GitBook Premium → $65/mo (if you need custom domain on product docs)

---

## Complete File Map (_Admin/Setup/)

| File | Part | Content |
|---|---|---|
| `00-MASTER-SETUP-GUIDE.md` | All | Overview + condensed summary of all parts |
| `01-Folder-Structure-Git-Cursor.md` | 1 | Folder structure, Git, Cursor/VS Code |
| `02-Obsidian-Setup.md` | 2 | Obsidian config, plugins, Sync, Publish, folder hiding |
| `03-GitBook-Free-Setup.md` | 3 | GitBook free tier, monorepo sync, Docs Sites |
| `04-Mintlify-Free-Setup.md` | 4 | Mintlify Hobby tier, docs.json, API playground, custom domain |
| `05-Publishing-Stack.md` | 5 | Hashnode, Featurebase, DNS records, per-product map |
| `06-Notion-Sync.md` | 6 | Make.com automation, Notion ↔ GitHub sync |
| `07-Skillplate-Courses.md` | 7 | Skillplate setup, courses, Synthesia video generation |
| `08-Password-Protection.md` | 8 | Protection options per platform, Cloudflare workarounds |
| `09-Maximizing-Free-Features.md` | 9 | Power moves for every tool in the stack |
| `10-Action-Plan.md` | 10 | This file — 3-week rollout checklist |

---

*Save to: C:\Zajaly\ZajalyDocs\_Admin\Setup\10-Action-Plan.md*
*Version: 1.0 — February 19, 2026*
