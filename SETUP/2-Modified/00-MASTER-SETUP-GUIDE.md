---
title: ZajalyDocs Master Setup Guide
type: guide
status: published
owner: Malek
tags: [setup, obsidian, gitbook, mintlify, notion, skillplate, publishing]
project: general
version: 1.0
created: 2026-02-18
updated: 2026-02-18
publish: false
---

# ZajalyDocs — Master Setup Guide

> Complete setup for the Zajaly documentation system: Obsidian (paid), GitBook (free), Mintlify (free), publishing stack, Notion sync, Skillplate courses, and video generation.

**Individual guide files:** Each section below also exists as a standalone file in `_Admin/Setup/`.

---

# PART 1: FOLDER STRUCTURE + GIT + CURSOR
📄 **Individual file:** [[01-Folder-Structure-Git-Cursor]]

---

## 1.1 — Folder Structure

The vault lives at `C:\Zajaly\ZajalyDocs` with 5 roots:

```
ZajalyDocs/
├── _Admin/                      # ZajalyDocs system config, tools, and internal assets
│   ├── Apps/                    # Utility scripts & integrations for this system
│   │   ├── notion-sync/         # Example: Notion ↔ Obsidian sync app
│   │   └── inbox-processor/     # Example: _Inbox/ automation
│   ├── Business/                # Contract templates, brand assets, ops notes
│   │   ├── Legal/
│   │   ├── Brand/
│   │   └── Operations/
│   ├── Setup/                   # These setup guides
│   ├── Scripts/
│   └── Config/
├── _Inbox/                      # Universal capture zone — drop anything, process weekly
├── _Sources/                    # Raw external reference material, organized BY TOPIC
│   ├── Servers/
│   ├── Laravel/
│   ├── SimpleBackups/
│   └── [any tool or topic]/
├── ZajContent/                  # Publishing outputs derived from ZajDocs
│   ├── Blog/                    # Posts → Hashnode (blog.zajaly.dev)
│   │   ├── Drafts/
│   │   └── Published/
│   └── Courses/                 # Skillplate scripts (EN / ES / AR)
│       ├── EN/
│       ├── ES/
│       └── AR/
├── ZajDocs/                     # ← Obsidian vault (map ONLY this folder)
│   ├── Guides/                  # Final how-tos, SOPs by tech topic
│   │   ├── Servers/
│   │   ├── Laravel/
│   │   ├── React/
│   │   ├── Python/
│   │   ├── Databases/
│   │   ├── Git-DevOps/
│   │   ├── APIs/
│   │   ├── AI-ML/
│   │   └── Security/
│   ├── Tools/                   # Reviews, comparisons, current stack
│   ├── Defaults/              # Snippets, cheatsheets, AI prompts, templates
│   └── _Archive/                # Outdated content, kept for reference
└── ZajProjects/                 # SaaS product knowledge
    ├── Custojo/
    ├── Waraq/
    ├── LMS/
    ├── ResiBoard/
    ├── RepoMemo/
    └── DeployVault/
```

**Root key:**

| Root | Purpose | Obsidian? |
|---|---|---|
| `_Admin/` | Vault setup, scripts, config | ❌ |
| `_Admin/Apps/` | Utility scripts & integrations for this system | ❌ |
| `_Admin/Business/` | Contract templates, brand, ops notes | ❌ |
| `_Inbox/` | Universal capture — process weekly | ❌ |
| `_Sources/` | External reference material, by topic | ❌ |
| `ZajContent/` | Blog posts + course scripts (derived from ZajDocs) | ❌ |
| `ZajDocs/` | Guides, tools, essentials — the Obsidian vault | ✅ |
| `ZajProjects/` | Per-product knowledge (Custojo, Waraq, etc.) | Selectively |

**Cross-topic rule:** Files live in one primary folder. Tags handle everything else:

```yaml
tags: [servers, backups, tools, SimpleBackups]
tool: SimpleBackups
```
Dataview query: `type:guide AND tags:SimpleBackups`

**Frontmatter on every file:**
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

Tags + Dataview queries let you find anything across folders:
- `type:guide AND tags:servers` → all server guides
- `tags:SimpleBackups` → everything about SimpleBackups regardless of folder
- `status:outdated` → everything needing review
- `project:custojo` → everything about Custojo

## 1.2 — Git Setup

### Initialize the repo (if not done):

```powershell
cd "C:\Zajaly\ZajalyDocs"
git init
git remote add origin https://github.com/rovony/ZajalyDocs.git
git add .
git commit -m "Initial vault setup"
git branch -M main
git push -u origin main
```

### .gitignore (already created at vault root):

```
.obsidian/workspace.json
.obsidian/workspace-mobile.json
.obsidian/cache/
.DS_Store
Thumbs.db
desktop.ini
.trash/
node_modules/
*.tmp
*.swp
*~
.env
*.key
```

## 1.3 — Cursor / VS Code Setup

Open `C:\Zajaly\ZajalyDocs\ZajDocs` in Obsidian — **map only the `ZajDocs/` subfolder as your vault**, not the full root.

**Create `.cursor/rules` directory** (Cursor will auto-read this):
```powershell
mkdir "C:\Zajaly\ZajalyDocs\.cursor"
```

The `.cursorrules` file at the vault root contains all AI rules for doc creation. Cursor reads this automatically.

**Recommended VS Code / Cursor extensions:**
- Markdown All in One — preview, TOC, shortcuts
- Markdown Preview Enhanced — better rendering
- markdownlint — catch formatting issues
- Foam — wikilink support, graph view
- Git Graph — visual git history
- YAML — frontmatter validation

---

# PART 2: OBSIDIAN SETUP (PAID: $4/mo Sync + $8/mo Publish)
📄 **Individual file:** [[02-Obsidian-Setup]]

---

## 2.1 — Install Obsidian

1. Go to **https://obsidian.md** → Download for Windows
2. Run installer, launch Obsidian
3. When asked → **Open folder as vault** → select `C:\Zajaly\ZajalyDocs`
4. This opens your existing folder structure as an Obsidian vault

## 2.2 — Configure Settings

**Settings → Editor:**
- Default editing mode → **Source mode** (markdown first)
- Show line numbers → ON
- Spellcheck → ON
- Readable line length → ON

**Settings → Files & Links:**
- Default location for new notes → **Same folder as current file**
- Use `[[Wikilinks]]` → ON
- Automatically update internal links → ON
- Default location for attachments → **In subfolder under current folder** (name it `_assets`)

**Settings → Appearance:**
- Theme → Browse → install **Minimal** → Use
- Install **Style Settings** plugin to customize Minimal

## 2.3 — Install Plugins

### Core plugins (Settings → Core plugins → toggle ON):
- Templates
- Tags view
- Backlinks
- Outline
- Word count
- Page preview
- Search
- Quick switcher

### Community plugins (Settings → Community plugins → Turn off restricted mode → Browse):

| Plugin | Purpose | Config |
|---|---|---|
| **Obsidian Git** | Auto-backup to GitHub | Backup every 30 min, auto-pull on startup |
| **Dataview** | Query docs like a database | Enable JavaScript queries |
| **Templater** | Advanced templates with variables | Template folder: `Defaults/Templates` |
| **Calendar** | Daily/weekly notes view | |
| **Folder Note** | Summary note per folder | |
| **Style Settings** | Customize Minimal theme | |
| **Tag Wrangler** | Rename/merge tags across vault | |
| **Linter** | Auto-format markdown on save | Enable YAML sort, heading blanks |

### Configure Obsidian Git:
1. Settings → Obsidian Git
2. Vault backup interval (minutes): **30**
3. Auto pull on startup: **ON**
4. Commit message: `vault backup: {{date}}`
5. Pull on startup: **ON**
6. Push on backup: **ON**

### Configure Templater:
1. Settings → Templater
2. Template folder location: `Defaults/Templates`
3. Trigger Templater on new file creation: **ON**

## 2.4 — Obsidian Sync ($4/mo)

Sync keeps your vault in sync across devices (PC, phone, tablet).

1. Go to **https://obsidian.md/account** → sign in or create account
2. Go to **https://obsidian.md/pricing** → purchase Sync Standard ($4/mo annual, $5/mo monthly)
3. In Obsidian: Settings → Sync → Log in
4. Create a new remote vault → name it `ZajalyDocs`
5. Select vault → enable sync
6. What to sync: **Everything EXCEPT** `.obsidian/workspace.json`
7. On other devices: install Obsidian → Set up Sync → connect to `ZajalyDocs` remote vault

**Note:** You now have TWO sync mechanisms — Git (for version control + GitHub backup) and Obsidian Sync (for seamless multi-device). They don't conflict. Git handles history/backup, Sync handles real-time device sync.

## 2.5 — Obsidian Publish ($8/mo)

Publish turns selected notes into a public website.

1. Go to **https://obsidian.md/pricing** → purchase Publish ($8/mo annual, $10/mo monthly)
2. In Obsidian: Settings → Publish → Log in
3. Click the **Publish** icon (paper plane) in the left ribbon
4. Select which notes/folders to publish (only files with `publish: true` in frontmatter)
5. Files NOT selected remain private

### Custom Domain Setup:

Your domain: `zajaly.dev` (Namecheap, DNS on Cloudflare)

1. In Obsidian Publish settings → Manage sites → Custom domain
2. Enter subdomain: e.g., `vault.zajaly.dev` or `notes.zajaly.dev`
3. In Cloudflare DNS:
   - Type: **CNAME**
   - Name: `vault` (or whatever subdomain)
   - Target: `publish-main.obsidian.md`
   - Proxy: **DNS only** (gray cloud, NOT orange)
4. Wait 15-60 min for propagation
5. Back in Obsidian → verify domain

### Password Protection:
1. Publish settings → Site options → Password
2. Set a password → all visitors must enter it
3. **Limitation:** This protects the ENTIRE published site. You cannot password-protect individual pages or folders. Everything published is behind one password.

### Publish Settings:
- Show graph view → ON (nice visual)
- Show navigation → ON
- Show search → ON
- Custom CSS → optional, paste custom CSS to style your site

---

# PART 3: GITBOOK FREE SETUP
📄 **Individual file:** [[03-GitBook-Free-Setup]]

> Full details, substeps, and free tier workarounds: see `03-GitBook-Free-Setup.md`

---

## Space vs Docs Site — Key Distinction

| | **Space** | **Docs Site** |
|---|---|---|
| What it is | Where you write & organize content | The published website readers see |
| Who sees it | Just you (editor) | The public (or your audience) |
| Analogy | GitHub repository | Deployed website |

**How they connect:** Space (edit) → Docs Site (publish). One Space = one Docs Site on free tier.

---

## 3.1 — Create Account

1. Go to **https://gitbook.com** → **Sign up with GitHub**
2. Create organization → name: `Zajaly`

---

## 3.2 — Create Spaces (Starting with 3)

| Space | Docs Site URL | Source (GitHub subfolder) | Audience |
|---|---|---|---|
| **ZajalyDocs** | `zajaly.gitbook.io/docs` | `/ZajDocs/Guides/` + `/ZajDocs/Tools/` | Public — knowledge base |
| **Custojo** | `zajaly.gitbook.io/custojo` | `/ZajProjects/Custojo/` | Customers |
| **Waraq** | `zajaly.gitbook.io/waraq` | `/ZajProjects/Waraq/` | Developers |

Add more spaces later (LMS, ResiBoard, RepoMemo, DeployVault) when ready.

For each space:
1. GitBook dashboard → **+** → **New space** → name it
2. Choose **Blank** to start

---

## 3.3 — Connect GitHub (Git Sync — Monorepo)

All spaces sync to **subfolders** of the same `rovony/ZajalyDocs` repo — no separate repos needed.

For each Space:
1. Space → **⚙ Settings** → **Integrations** → **GitHub**
2. Authorize GitBook (first time only)
3. Select repo: `rovony/ZajalyDocs` | Branch: `main`
4. Set **monorepo path** (subfolder):
   - ZajalyDocs → `/Docs`
   - Custojo → `/ZajProjects/Custojo`
   - Waraq → `/ZajProjects/Waraq`
5. Sync direction: **GitHub → GitBook** (Git is source of truth)
6. Click **Sync** → GitBook imports existing files

Now: push to GitHub → GitBook auto-syncs within ~1 min.

---

## 3.4 — Create Docs Sites (Publish)

For each Space:
1. GitBook dashboard → **Docs Sites** → **+ New site**
2. Connect to matching Space
3. Audience: **Public**
4. Click **Publish** → live at `zajaly.gitbook.io/[slug]`

---

## 3.5 — Content Structure

Create `README.md` in every folder — GitBook uses it as the section home page.
Create `SUMMARY.md` in each Space root to control sidebar navigation order.

See `03-GitBook-Free-Setup.md` → Step 8 for full `SUMMARY.md` example.

---

## 3.6 — Password Protection Workarounds (Free)

Native password protection = $249/site/mo (Ultimate). Not worth it.

| Option | How | Cost |
|---|---|---|
| **Unlisted link** | Docs Site → Audience → Unlisted | Free — hidden but not password-protected |
| **Cloudflare Zero Trust** | Requires custom domain + Cloudflare | Free up to 50 users |
| **Cloudflare Pages + Worker** | Export to static site → add Worker auth | Free, `*.pages.dev` |

**For now:** Keep ZajalyDocs as **Unlisted**, product docs (Custojo, Waraq) as **Public**.

---

## 3.7 — Free Tier Summary

| Feature | Free |
|---|---|
| Spaces | ✅ Unlimited |
| Public Docs Sites | ✅ Unlimited |
| `*.gitbook.io` domain | ✅ |
| Git sync | ✅ |
| Custom domain | ❌ ($65/site/mo) |
| Password protection | ❌ ($249/site/mo) |
| Multiple editors | ❌ (1 editor free) |


**Your URL will be:** `zajaly.gitbook.io/[space-name]`
Custom domain like `docs.custojo.com` requires upgrading to $65/site/mo.

---

# PART 4: MINTLIFY FREE SETUP
📄 **Individual file:** [[04-Mintlify-Free-Setup]]

---

> **Honest note:** Mintlify is designed for developer API docs, not SOPs or general guides. Its free tier has one killer advantage: custom domain at $0. Use it for `docs.zajaly.dev` if you want a polished dev-facing site.

## 4.1 — Create Account

1. Go to **https://mintlify.com** → Sign up with GitHub
2. Create new project → name: `zajaly-docs`
3. Mintlify creates a GitHub repo automatically

## 4.2 — Clone Locally

```powershell
cd "C:\Zajaly\Projects"
git clone https://github.com/rovony/zajaly-docs.git mintlify-docs
cd mintlify-docs
```

## 4.3 — Install Mintlify CLI

```powershell
npm install -g mintlify
mintlify dev
```

Preview at `http://localhost:3000`

## 4.4 — Configure `mint.json`

```json
{
  "name": "Zajaly Docs",
  "logo": {
    "light": "/logo/light.png",
    "dark": "/logo/dark.png"
  },
  "favicon": "/favicon.png",
  "colors": {
    "primary": "#0A84FF",
    "light": "#4DA6FF",
    "dark": "#0066CC"
  },
  "navigation": [
    {
      "group": "Getting Started",
      "pages": ["index", "getting-started/quickstart"]
    },
    {
      "group": "Guides",
      "pages": ["guides/overview"]
    }
  ]
}
```

## 4.5 — Custom Domain (FREE on Mintlify)

This is the reason to use Mintlify — free custom domain.

1. Mintlify Dashboard → Your project → Settings → Custom domain
2. Enter: `docs.zajaly.dev`
3. In Cloudflare DNS:
   - Type: **CNAME**
   - Name: `docs`
   - Target: `cname.mintlify.com`
   - Proxy: **DNS only** (gray cloud)
4. Wait 15 min → auto-verified

## 4.6 — Deploy

Push to GitHub → Mintlify auto-deploys. That's it.

```powershell
git add .
git commit -m "Initial docs setup"
git push origin main
```

## 4.7 — Free Tier Limitations

| Feature | Available? |
|---|---|
| Custom domain | ✅ Free |
| Git sync | ✅ Free |
| MDX/React components | ✅ Free |
| API playground | ✅ Free |
| Basic analytics | ✅ Free |
| AI writing assistant | ❌ $300/mo Pro |
| Password protection | ❌ $300/mo Pro |
| Collaboration | ❌ 1 editor only |
| AI agent | ❌ $300/mo Pro |

---

# PART 5: PUBLISHING STACK (Help Docs + Changelog + Blog)
📄 **Individual file:** [[05-Publishing-Stack]]

---

## 5.1 — The Goal

For each SaaS product, you need:
1. **Help docs** — product documentation for customers
2. **Changelog** — what's new, what changed
3. **Blog** — articles, tutorials, thought leadership

All free, with custom domains where possible.

## 5.2 — Recommended Free Stack

### Help Docs → Mintlify (docs.zajaly.dev) or Docusaurus on Vercel

**Option A: Mintlify** (already set up in Part 4)
- Free custom domain ✅
- Beautiful output
- Best for: developer-facing docs

**Option B: Docusaurus on Vercel** (free, full control)
```powershell
npx create-docusaurus@latest custojo-help classic
cd custojo-help
npm run start
# Deploy: push to GitHub → connect to Vercel → custom domain
```
- Free custom domain via Vercel ✅
- React-based (your stack)
- Full control, self-hosted
- Best for: user-facing help centers

### Changelog → Featurebase (FREE with custom domain)

1. Go to **https://featurebase.app** → Create account
2. Create workspace: `Custojo`
3. Set subdomain: `custojo.featurebase.app`
4. Settings → Custom domain → `changelog.custojo.com`
5. In Cloudflare: CNAME `changelog` → as shown in Featurebase settings
6. Start posting updates

**Bonus:** Featurebase also gives you a feedback board + roadmap for free.

### Blog → Hashnode (FREE with custom domain)

1. Go to **https://hashnode.com** → Create account
2. Create publication: `Zajaly Blog` (or per-product)
3. Settings → Domain → connect `blog.zajaly.dev`
4. In Cloudflare: CNAME `blog` → `hashnode.network`
5. Free forever, custom domain free ✅

**Alternative: Ghost self-hosted** on your VPS (free, more control):
```bash
npm install ghost-cli@latest -g
mkdir zajaly-blog && cd zajaly-blog
ghost install
```

## 5.3 — Per-Product Stack

```
Custojo
├── Help docs  → Mintlify or Docusaurus → docs.custojo.com (FREE) [ZajProjects/Custojo/]
├── Changelog  → Featurebase → changelog.custojo.com (FREE) [ZajProjects/Custojo/Changelog.md]
└── Blog       → Hashnode → blog.custojo.com (FREE) [ZajContent/Blog/]

Waraq.dev
├── Help docs  → Mintlify → docs.waraq.dev (FREE) [ZajProjects/Waraq/]
├── Changelog  → Featurebase → changelog.waraq.dev (FREE) [ZajProjects/Waraq/Changelog.md]
└── Blog       → Hashnode (shared or separate) [ZajContent/Blog/]

General / Zajaly
├── Knowledge  → Obsidian Publish → vault.zajaly.dev ($8/mo, password protected)
├── Dev docs   → Mintlify → docs.zajaly.dev (FREE)
├── Blog       → Hashnode → blog.zajaly.dev (FREE) [ZajContent/Blog/]
├── Courses    → Skillplate → learn.zajaly.dev (lifetime) [ZajContent/Courses/]
└── GitBook    → zajaly.gitbook.io (FREE, no custom domain)
```

## 5.4 — Domain Setup Summary (zajaly.dev on Cloudflare)

| Subdomain | Points to | Service | Cost |
|---|---|---|---|
| `docs.zajaly.dev` | `cname.mintlify.com` | Mintlify | Free |
| `vault.zajaly.dev` | `publish-main.obsidian.md` | Obsidian Publish | $8/mo |
| `blog.zajaly.dev` | `hashnode.network` | Hashnode | Free |
| `changelog.zajaly.dev` | Featurebase CNAME | Featurebase | Free |

All CNAME records in Cloudflare, DNS only (gray cloud).

---

# PART 6: NOTION SYNC
📄 **Individual file:** [[06-Notion-Sync]]

---

## 6.1 — The Honest Truth

No tool in this stack has native bidirectional Notion sync. Here's what actually works:

## 6.2 — Best Available: Make.com Automation (Free Tier)

Make.com free tier = 1,000 operations/month. Enough for periodic sync.

### Notion → Obsidian (via GitHub):

1. Create Make account (make.com)
2. Create scenario:
   - **Trigger:** Notion → Watch Database Items
   - **Action:** GitHub → Create or Update File
3. The file lands in your `rovony/ZajalyDocs` repo
4. Obsidian Git plugin pulls it on next sync (every 30 min)
5. Result: new/updated Notion pages appear in Obsidian within ~30 min

### Obsidian → Notion:

1. Obsidian Git auto-commits and pushes to GitHub
2. Make scenario:
   - **Trigger:** GitHub → Watch Repository Events (push)
   - **Action:** Notion → Create or Update Database Item
3. Result: new vault notes appear in Notion within ~15 min

### Setup Time: ~2 hours. Cost: $0.

## 6.3 — Alternative: obsidianotion Plugin

- Community plugin: search `obsidianotion` in Obsidian plugin browser
- Pulls Notion pages INTO your vault (one-way: Notion → Obsidian)
- Requires Notion API key: Notion → Settings → Connections → Develop → New integration
- Best for: one-time migration of existing Notion content

## 6.4 — Recommended Architecture

```
Notion (write/collaborate here)
    ↓ Make.com (every 15 min)
GitHub (source of truth)
    ↓ automatic
Obsidian vault (local copy via Git plugin)
    AND
GitBook (published docs via Git sync)
    AND
Mintlify (dev docs via Git sync)
```

## 6.5 — For GitBook ↔ Notion

No native integration. Workaround:
- GitBook → GitHub (native sync) → Make → Notion

## 6.6 — For Mintlify ↔ Notion

No integration. Mintlify is MDX files in GitHub.
- Make: Notion → export as markdown → push to GitHub → Mintlify auto-deploys

---

# PART 7: SKILLPLATE + COURSES + VIDEO GENERATION
📄 **Individual file:** [[07-Skillplate-Courses]]

---

## 7.1 — Skillplate Overview (Tier 4 — Growth Plan)

You have the Tier 4 lifetime deal from AppSumo ($349 one-time). This gives you:

- AI course builder (auto-generates course structure from a topic)
- Website builder with landing pages
- CRM for students/leads
- Stripe integration for payments
- Video lessons, text lessons, file downloads
- Quizzes and certifications
- Analytics and progress tracking
- 180+ app integrations
- Custom domain support
- Multi-language support (English, Spanish, Arabic — all supported)

### Setup Steps:

1. Go to **https://skillplate.com** → Log in with your AppSumo credentials
2. Create your first academy / workspace
3. Settings → Custom domain → connect `learn.zajaly.dev` or `courses.custojo.com`
4. In Cloudflare: CNAME as shown in Skillplate settings
5. Create your first course using AI Course Builder:
   - Enter topic → AI generates course structure
   - Review and edit modules/lessons
   - Add content: text, video, files, quizzes

### Integration with ZajalyDocs:

Your course content drafts live in `C:\Zajaly\ZajalyDocs\ZajContent\Courses\`:

```
ZajContent/
└── Courses/
    ├── EN/
    │   ├── Server-Setup-101/
    │   │   ├── 00-Course-Overview.md
    │   │   ├── 01-Lesson-VPS-Basics.md
    │   │   ├── 02-Lesson-SSH-Setup.md
    │   │   └── 03-Lesson-Security.md
    │   └── Laravel-Fundamentals/
    │       ├── 00-Course-Overview.md
    │       └── ...
    ├── ES/
    └── AR/
```

Write lesson content derived from `ZajDocs/Guides/` → finalize in Skillplate.

## 7.2 — AI Video Generation for Course Lessons

For no-human video lessons (AI avatar speaks your script):

### Recommended: Synthesia

**What it does:** You type a script → choose an AI avatar → get a professional video of the avatar speaking your content. 240+ avatars, 160+ languages.

**Pricing (2026):**
- Free: 3 minutes/month, watermarked
- Starter: $18/mo annual ($22/mo monthly) — 10 min/month
- Creator: $64/mo annual — 30 min/month
- Enterprise: custom pricing — unlimited

**Workflow:**
1. Write lesson script in the Course-Lesson-Template's "Video Script" section
2. Go to synthesia.io → paste script → select avatar → select language
3. Generate video → download MP4
4. Upload to Skillplate lesson

**Best for:** Clean, professional talking-head lessons. Corporate training style.

### Alternative: HeyGen (similar, slightly cheaper)

- $24/mo for 15 min
- Good lip-sync and avatar realism
- Supports multi-language dubbing

### Free/Budget Alternative: Veed.io + AI Voice

If Synthesia is too expensive to start:
1. Create slides/visuals (Canva, PowerPoint)
2. Use ElevenLabs (elevenlabs.io) free tier for AI voiceover
3. Use Veed.io free tier to combine visuals + voiceover
4. Result: slide-based video with AI narration, no avatar

### Multi-Language Course Videos:

With Synthesia, the same avatar can speak any of 160+ languages. Your workflow:
1. Write script in English
2. Generate English video
3. In Synthesia → Translate → select Spanish/Arabic
4. One-click generates the localized version

Upload each language version to the appropriate Skillplate course.

## 7.3 — Skillplate Local Folder

```
_Admin/Apps/Skillplate/
├── README.md              # How the Skillplate integration works
├── Course-Ideas.md        # Course pipeline
├── AI-Course-Builder.md   # Tips for using Skillplate's AI
└── Video-Workflow.md      # Steps for video generation
```

---

# PART 8: PASSWORD PROTECTION SUMMARY
📄 **Individual file:** included here

---

| Platform | Password Protection | How |
|---|---|---|
| **Obsidian Publish** ($8/mo) | ✅ Entire site | Publish settings → Password → set one password |
| **GitBook Free** | ❌ Not available | Requires Ultimate ($249/mo) |
| **Mintlify Free** | ❌ Not available | Requires Pro ($300/mo) |
| **Hashnode** | ❌ No | All posts are public |
| **Featurebase** | ⚠️ Partial | Can set visibility per board |
| **Skillplate** | ✅ Per course | Courses can be free, paid, or invite-only |

**Best option for private docs:** Obsidian Publish ($8/mo) with site-wide password. This is the only affordable password protection you get across all these tools.

---

# PART 9: MAXIMIZING FREE FEATURES
📄 **Individual file:** included here

---

## Obsidian ($4 Sync + $8 Publish = $12/mo total)

**Sync features:**
- End-to-end AES-256 encryption
- Sync across unlimited devices (PC, phone, tablet)
- Version history for every note
- Selective sync (choose which folders to sync)
- 10 GB per vault

**Publish features:**
- Custom domain ✅
- Password protection (whole site) ✅
- Graph view for visitors ✅
- Navigation sidebar ✅
- Search ✅
- Custom CSS ✅
- Selective publishing (choose which files)
- SEO-friendly URLs

**Power moves:**
- Use Dataview to create auto-generated index pages (e.g., "all published guides")
- Use CSS snippets to brand your published site
- Use the Graph View as a visual navigation tool for readers
- Combine publish + password for a private team knowledge base

## GitBook Free

- Unlimited public spaces ✅
- Full version history ✅
- Git sync (bidirectional with GitHub) ✅
- Clean, professional published output ✅
- Table of contents auto-generated ✅
- Markdown + rich blocks ✅
- Search ✅

**Power moves:**
- Use Git sync to edit in VS Code/Cursor AND GitBook interchangeably
- Create separate spaces per product for organized publishing
- Use GitBook's SUMMARY.md to control navigation structure

## Mintlify Free

- Custom domain ✅
- API playground (interactive API testing for readers) ✅
- MDX support (React components in docs) ✅
- Git-native deployment ✅
- Beautiful default theme ✅

**Power moves:**
- Use the API playground to let users test your API endpoints live
- Use MDX components (Steps, Cards, Tabs) for rich documentation
- Deploy to `docs.zajaly.dev` for your primary dev-facing docs

---

# PART 10: ACTION PLAN
📄 **Individual file:** included here

---

## Week 1 — Foundation (do this first)

1. ✅ Confirm folder structure at `C:\Zajaly\ZajalyDocs`
2. ✅ Initialize Git, push to `github.com/rovony/ZajalyDocs`
3. ✅ Create `.cursorrules` and `.gitignore`
4. ✅ Open vault in Obsidian → configure settings (Section 2.2)
5. ✅ Install all plugins (Section 2.3)
6. ✅ Set up Obsidian Sync ($4/mo) → test on phone
7. ✅ Set up Obsidian Publish ($8/mo) → connect `vault.zajaly.dev`
8. ✅ Set password on Publish site
9. ✅ Create first 3 guides using templates

## Week 2 — Publishing

10. ✅ Create GitBook account → create Custojo Docs space → connect GitHub
11. ✅ Create Mintlify project → connect `docs.zajaly.dev`
12. ✅ Create Featurebase account → Custojo changelog
13. ✅ Create Hashnode blog → connect `blog.zajaly.dev`
14. ✅ Set up all DNS records in Cloudflare

## Week 3 — Sync + Courses

15. ✅ Set up Make.com → Notion ↔ GitHub automation
16. ✅ Test full sync: Notion → GitHub → Obsidian → GitBook
17. ✅ Activate Skillplate → create first course structure
18. ✅ Test Synthesia free tier → generate sample lesson video

## Month 2 — Optimize

19. Evaluate: which publishing tools are you actually using?
20. First real Servers/Setup guide series
21. First tool comparison
22. First course published on Skillplate

---

## Monthly Cost Summary

| Tool | Cost | Purpose |
|---|---|---|
| Obsidian app | Free | Local editor |
| Obsidian Sync | $4/mo | Multi-device sync |
| Obsidian Publish | $8/mo | Published site + password + custom domain |
| GitHub | Free | Version control + backup |
| GitBook | Free | Product docs (gitbook.io subdomain) |
| Mintlify | Free | Dev docs (custom domain) |
| Featurebase | Free | Changelog + feedback |
| Hashnode | Free | Blog (custom domain) |
| Skillplate | $0 (lifetime) | Courses |
| Make.com | Free | Notion sync (1,000 ops/mo) |
| **Total** | **$12/mo** | Complete documentation system |

Optional later:
- Synthesia Starter → $18/mo (for course videos)
- GitBook Premium → $65/mo (if you need custom domain on product docs)

---

*Save to: C:\Zajaly\ZajalyDocs\_Admin\Setup\00-MASTER-SETUP-GUIDE.md*
*Last updated: February 18, 2026*
