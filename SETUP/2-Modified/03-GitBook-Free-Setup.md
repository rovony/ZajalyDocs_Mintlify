---
title: GitBook Free Setup — Complete Guide
type: guide
status: published
owner: Malek
tags: [setup, gitbook, publishing, docs]
project: general
version: 2.0
created: 2026-02-19
updated: 2026-02-19
publish: false
---

# GitBook Free Setup — Complete Guide

> Free tier. Unlimited public sites. Git sync. No credit card needed.

---

## Space vs Docs Site — What's the Difference?

This is the most confusing part of GitBook. Here's the simple version:

| | **Space** | **Docs Site** |
|---|---|---|
| **What it is** | Your working area — where you write and organize content | The published website your readers see |
| **Who sees it** | Just you (the editor) | The public (or invited audience) |
| **Analogy** | A GitHub repository | A deployed website |
| **Relationship** | A Docs Site pulls content from one or more Spaces | One Docs Site = one published URL |

**In practice:**
1. You create a **Space** → write and organize pages inside it
2. You create a **Docs Site** → link it to your Space → publish it
3. On free tier: 1 Docs Site per Space, all on `*.gitbook.io`

> [!NOTE]
> You can link **multiple Spaces** into one Docs Site (paid feature — "site sections"). On free, it's 1 Space → 1 Docs Site.

---

## Our GitBook Setup

### Current Folder Layout (relevant parts)

```
ZajalyDocs/                       ← Git repo root (rovony/ZajalyDocs)
├── ZajDocs/                      ← ZajalyDocs GitBook space (guides + tools)
│   ├── .gitbook.yaml          # GitBook config
│   ├── README.md              # Space homepage
│   ├── SUMMARY.md             # Sidebar navigation
│   ├── Guides/                # Servers, Laravel, React, etc.
│   ├── Tools/                 # Reviews, comparisons, current stack
│   ├── Defaults/              # Snippets, cheatsheets, templates
│   └── _Archive/
├── ZajProjects/                  ← Each product = its own GitBook space
│   ├── Custojo/
│   ├── Waraq/
│   ├── LMS/
│   ├── ResiBoard/
│   ├── RepoMemo/
│   └── DeployVault/
├── ZajContent/                   # Blog, courses (not on GitBook)
├── _Admin/                       # Setup guides, scripts (never published)
├── _Inbox/
└── _Sources/
```

### Spaces & Sites (Starting With 3)

| Space | Docs Site URL | Git Sync Path (monorepo) | Audience |
|---|---|---|---|
| **ZajalyDocs** | `zajaly.gitbook.io/docs` | `/ZajDocs` | Public — guides, tools, knowledge base |
| **Custojo** | `zajaly.gitbook.io/custojo` | `/ZajProjects/Custojo` | Customers |
| **Waraq** | `zajaly.gitbook.io/waraq` | `/ZajProjects/Waraq` | Developers |

Add more spaces later (LMS, ResiBoard, RepoMemo, DeployVault) when those products need docs.

> [!NOTE]
> **Why this works with zero overlap:** ZajProjects lives outside ZajDocs/, so each space points to a completely separate folder tree. No parent/child conflicts. ZajalyDocs gets `/ZajDocs` (including Guides + Tools), product spaces get `/ZajProjects/[name]`.

---

## Step 1 — Create Your GitBook Account

1. Go to **https://gitbook.com** → **Sign up with GitHub** (easiest — Git sync works seamlessly)
2. Create organization → name: `Zajaly`
3. GitBook creates a default workspace

---

## Step 2 — Prepare Your GitHub Repo for Monorepo Sync

All GitBook spaces sync to **subfolders of the same repo** (`rovony/ZajalyDocs`). No separate repos needed.

### 2A — Create a `.gitbook.yaml` in EACH synced folder

GitBook looks for `.gitbook.yaml` inside the project directory to know how to parse content. Create one in each folder that will be synced:

**`ZajDocs/.gitbook.yaml`**
```yaml
root: ./

structure:
  readme: README.md
  summary: SUMMARY.md
```

**`ZajProjects/Custojo/.gitbook.yaml`**
```yaml
root: ./

structure:
  readme: README.md
  summary: SUMMARY.md
```

**`ZajProjects/Waraq/.gitbook.yaml`**
```yaml
root: ./

structure:
  readme: README.md
  summary: SUMMARY.md
```

### 2B — Create a `README.md` in each space root

GitBook uses `README.md` as the homepage for each space. If it doesn't exist, GitBook will create one on first sync (which can cause unexpected commits).

Only the **space root** README.md is required. Subfolder READMEs are optional — create them only for major sections that deserve a landing page. See "Folder README.md" in Step 6 for guidance.

Create these now:

**`ZajDocs/README.md`**
```markdown
---
description: Step-by-step technical guides, tool reviews, cheatsheets, and references for the Zajaly development stack.
---

# Zajaly Docs

Step-by-step technical guides, tool reviews, cheatsheets, and references for the Zajaly development stack.
```

**`ZajProjects/Custojo/README.md`**
```markdown
---
description: Everything you need to get started with Custojo CRM.
---

# Custojo Documentation

Everything you need to get started with Custojo CRM.
```

**`ZajProjects/Waraq/README.md`**
```markdown
---
description: Developer documentation for the Waraq cloud IDE.
---

# Waraq.dev Documentation

Developer documentation for the Waraq cloud IDE.
```

> [!NOTE]
> **Frontmatter `description`** — GitBook uses this field for SEO meta tags and link previews. Keep it under 160 characters. GitBook also recognizes `icon:` (a FontAwesome icon name) for the sidebar. All other ZajalyDocs frontmatter fields (`title`, `type`, `status`, `tags`, etc.) are preserved in Git but ignored by GitBook.

> [!CAUTION]
> **Never create or rename README.md files through the GitBook UI** when Git Sync is enabled. Always manage README files directly in your Git repository. Creating them through GitBook UI causes sync conflicts.

### 2C — Commit these files

```powershell
cd "C:\Zajaly\ZajalyDocs"
git add ZajDocs/.gitbook.yaml ZajDocs/README.md
git add ZajProjects/Custojo/.gitbook.yaml ZajProjects/Custojo/README.md
git add ZajProjects/Waraq/.gitbook.yaml ZajProjects/Waraq/README.md
git commit -m "Add GitBook config files for all spaces"
git push origin main
```

### 2D — Redirects (add later when renaming/moving pages)

When you rename or move a published page, Git creates a new file and deletes the old one — GitBook cannot detect renames. The old URL returns 404. Add redirects to `.gitbook.yaml` to fix this:

```yaml
root: ./

structure:
  readme: README.md
  summary: SUMMARY.md

redirects:
  old-folder/old-page: new-folder/new-page.md
  guides/setup: guides/servers/setup/vps-setup.md
```

Rules for redirects:
- Key = old path (without leading `/`), Value = new file path (relative to root)
- The old page must be **removed** — redirects only fire if no page exists at the old path
- Use a YAML linter to validate; bad indentation silently breaks redirects
- Always add a redirect when renaming or moving a published page

---

## Step 3 — Create Spaces in GitBook

For each of the 3 spaces:

1. GitBook dashboard → left sidebar → **+** → **New space**
2. Name it (e.g., `ZajalyDocs`)
3. Choose **Blank** — we'll import from GitHub in the next step

Repeat for `Custojo` and `Waraq`.

---

## Step 4 — Connect Git Sync (GitHub — Monorepo)

> Do this for each Space separately.

1. Open Space → top-right **⚙ Settings** → **Integrations** → **GitHub**
2. **Authorize GitBook** on GitHub (first time only — grants repo access)
3. Select repo: `rovony/ZajalyDocs`
4. Select branch: `main`
5. Set **Project directory** (monorepo path):
   - ZajalyDocs Space → `ZajDocs`
   - Custojo Space → `ZajProjects/Custojo`
   - Waraq Space → `ZajProjects/Waraq`
6. Sync direction: **GitHub → GitBook** (Git is source of truth for initial import)
7. Click **Sync** → GitBook imports existing files from that folder

### What happens after initial sync:

Git Sync is **bidirectional once connected**, regardless of which direction you chose for the initial import. After setup:

- Edit in Cursor/VS Code → push to GitHub → GitBook auto-syncs within ~1 min
- Edit in GitBook editor → auto-commits to GitHub → Obsidian Git pull picks it up

> [!TIP]
> The "sync direction" setting only controls which side wins during the **first sync** (in case both already have content). After that, it's always bidirectional.

---

## Step 5 — Create Docs Sites (Publish)

Each Space needs a Docs Site to be publicly accessible.

1. GitBook dashboard → **Docs Sites** (left sidebar) → **+ New site**
2. Name: `ZajalyDocs` (or `Custojo`, `Waraq`)
3. Connect to Space: select the matching Space
4. **Set the URL slug:** Under site settings, set the slug to control your URL:
   - ZajalyDocs → slug: `docs` → URL becomes `zajaly.gitbook.io/docs`
   - Custojo → slug: `custojo` → URL becomes `zajaly.gitbook.io/custojo`
   - Waraq → slug: `waraq` → URL becomes `zajaly.gitbook.io/waraq`
5. Audience: **Public** (free tier = public only)
6. Click **Publish**

---

## Step 6 — Structure Your Content

### ZajalyDocs Space (syncs to `ZajDocs/`)

```
ZajDocs/
├── .gitbook.yaml          ← GitBook config (required)
├── README.md              ← Space homepage (required)
├── SUMMARY.md             ← Sidebar navigation (required — see Step 8)
├── Guides/
│   ├── Servers/
│   │   ├── README.md      ← Section overview (major section → has landing page)
│   │   ├── Setup/
│   │   │   └── vps-setup.md
│   │   ├── SSH/
│   │   │   └── ssh-keys.md
│   │   └── Security/
│   │       └── hardening.md
│   ├── Laravel/
│   │   └── ...
│   └── React/
│       └── ...
├── Tools/
│   ├── Reviews/
│   │   └── tool-name.md
│   └── Comparisons/
│       └── tool-a-vs-b.md
└── Defaults/
    └── Cheatsheets/
        └── ...
```

### Product Space — Custojo (syncs to `ZajProjects/Custojo/`)

```
ZajProjects/Custojo/
├── .gitbook.yaml          ← Required
├── README.md              ← Required (product homepage)
├── SUMMARY.md             ← Required
├── getting-started.md
├── features/
│   ├── crm-module.md
│   └── pipelines.md
├── api-reference.md
├── changelog.md
└── faq.md
```

> [!IMPORTANT]
> **Only the space root `README.md` is required.** GitBook uses it as the homepage. Subfolder `README.md` files are optional — create them only for major sections that deserve a landing page (e.g., `Guides/Servers/README.md`). For leaf folders with 1-2 pages, the SUMMARY.md heading is enough to group them.
>
> **Always manage `README.md`, `SUMMARY.md`, and `.gitbook.yaml` in Git, not the GitBook UI** — editing them in GitBook's UI while Git Sync is active causes conflicts.

> [!TIP]
> **`_Archive/` and `Defaults/Templates/` are inside `ZajDocs/` and WILL sync to GitBook.** That's fine — just don't list them in `SUMMARY.md` and they won't appear in the sidebar navigation. They'll exist in the space but be invisible to readers. If you want to completely exclude folders from syncing, you'd need to move them outside `ZajDocs/`.

---

## Step 7 — Customize Your Docs Site

In each Docs Site settings:

- **Title** → set product/space name
- **Logo** → upload your logo (SVG or PNG)
- **Favicon** → upload favicon
- **Colors** → set primary brand color
- **Navigation** → auto-generated from SUMMARY.md or folder structure
- **Social links** → GitHub, Twitter, etc.
- **Footer** → copyright, links

### Free Integrations to Add

Space → **⚙ Settings** → **Integrations** → install any below:

| Integration | What It Does | Setup |
|---|---|---|
| **Fathom Analytics** | Privacy-friendly traffic stats | Add Fathom site ID (requires Fathom account) |
| **Plausible** | Privacy-friendly analytics | Add Plausible domain |
| **Amplitude** | Track page visits & identify users | Add API key |
| **Crisp** | Live chat widget on your docs | Add Crisp website ID (free Crisp plan works) |
| **Formspree** | Collect signups/feedback in docs | Add form ID (free tier: 50 submissions/mo) |
| **Arcade** | Embed interactive product demos | Paste Arcade embed URL |
| **Guideflow** | Add interactive guides/tours | Paste embed code |
| **Figma** | Embed Figma designs inline | Paste Figma file URL |
| **GitHub Files** | Show code from GitHub inline | Repo + file path |

> [!NOTE]
> These integrations are **free to install in GitBook**, but some (Fathom, Amplitude, Crisp) require their own accounts — check their individual free tiers.
>
> **Authenticated Access integrations (Auth0, Okta, Azure, OIDC) require Ultimate plan ($249/mo).** They appear in the marketplace and can be installed during a free trial, but will stop enforcing auth after the trial ends.

---

## Step 8 — SUMMARY.md (Table of Contents)

GitBook uses `SUMMARY.md` to define sidebar navigation order. **If you don't create one, GitBook auto-generates it** from folder structure on first sync (which may not match the order you want).

Create `SUMMARY.md` inside each synced folder:

### Format Rules

```markdown
# Summary

## Section Name        ← H2 = top-level sidebar group

- [Page Title](relative/path.md)
  - [Nested Page](relative/path/nested.md)

### Subsection Name    ← H3 = nested group within a section

- [Another Page](another.md)
```

- H1 (`#`) — file title, use `# Summary` or `# Table of contents`
- H2 (`##`) — top-level sidebar groups
- H3 (`###`) — nested sidebar groups within a section
- List items (`-` or `*`) — pages; indent 2-4 spaces for nesting under a parent page
- Links — always relative paths from the space root
- GitBook's official examples use `*` but `-` also works

### Page Link Titles (Sidebar Override)

To show a different title in the sidebar than the page's H1:

```markdown
* [Full Page Title](page.md "Short Sidebar Title")
```

The quoted text overrides the sidebar, pagination buttons, and relative link text. Optional — if omitted, the page's main title is used everywhere.

### No Duplicate Pages

A `.md` file can only appear **once** in SUMMARY.md. Listing the same file under two sections causes sync errors because it implies one page at two different URLs.

### Folder README.md — Two Valid Patterns

**With subfolder README.md** (section has its own overview/landing page):

```markdown
### Servers

- [Server Guides](Guides/Servers/README.md)
  - [VPS Setup](Guides/Servers/Setup/vps-setup.md)
  - [SSH Keys](Guides/Servers/SSH/ssh-keys.md)
```

**Without subfolder README.md** (heading groups pages directly):

```markdown
### Servers

- [VPS Setup](Guides/Servers/Setup/vps-setup.md)
- [SSH Keys](Guides/Servers/SSH/ssh-keys.md)
```

Create a subfolder README.md when the folder is a **major section** that deserves a landing page. Skip it for **leaf folders** with 1-2 pages — the SUMMARY.md heading is enough.

### Example — `ZajDocs/SUMMARY.md`

```markdown
# Summary

## Getting Started

- [Overview](README.md)

## Guides

### Servers

- [Server Guides](Guides/Servers/README.md)
  - [VPS Setup](Guides/Servers/Setup/vps-setup.md)
  - [SSH Keys](Guides/Servers/SSH/ssh-keys.md)
  - [Security Hardening](Guides/Servers/Security/hardening.md)

### Laravel

- [Laravel Guides](Guides/Laravel/README.md)

### React

- [React Guides](Guides/React/README.md)

## Tools

- [Tool Reviews](Tools/Reviews/README.md)
- [Comparisons](Tools/Comparisons/README.md)

## Defaults

- [Cheatsheets](Defaults/Cheatsheets/README.md)
```

### Example — `ZajProjects/Custojo/SUMMARY.md`

```markdown
# Summary

## Getting Started

- [Overview](README.md)
- [Quick Start](getting-started.md)

## Features

- [CRM Module](features/crm-module.md)
- [Pipelines](features/pipelines.md)

## Reference

- [API Reference](api-reference.md)
- [FAQ](faq.md)
- [Changelog](changelog.md)
```

### When to Update SUMMARY.md

| Action | SUMMARY.md Change |
|---|---|
| Add a new page | Add a `- [Title](path.md)` entry in the correct section |
| Rename a file | Update the path in the existing entry |
| Move a file | Update the path + add a redirect in `.gitbook.yaml` |
| Delete a page | Remove the entry |
| Reorder sidebar | Reorder the list items |
| Add a new folder | Use a `## Section` or `### Subsection` heading, OR add a folder README.md as the parent entry |

> [!TIP]
> **Only pages listed in SUMMARY.md appear in the sidebar navigation.** Files that exist in the repo but aren't in SUMMARY.md are still synced to the space but won't show in navigation. This is useful for keeping draft files in Git without publishing them.

> [!CAUTION]
> If you add a new markdown file to your repo but forget to add it to SUMMARY.md, it **won't appear** in GitBook's sidebar — even though it's synced. Always update SUMMARY.md when adding new pages.

---

## Step 8.5 — GitBook-Specific Markdown (Content Blocks)

GitBook extends standard Markdown with special blocks using Liquid-style `{% %}` tags and some HTML patterns. These render nicely in GitBook but appear as raw text in other renderers (Obsidian, GitHub).

### Links — Critical Rule

GitBook does **NOT** support Obsidian wikilinks. Always use relative markdown links:

- **Correct:** `[VPS Setup](Guides/Servers/Setup/vps-setup.md)`
- **Wrong:** `[[vps-setup]]`

### Code Blocks

Always specify a language for syntax highlighting:

````markdown
```bash
echo "hello"
```
````

For titled code blocks (renders with a filename header in GitBook):

```
{% code title="nginx.conf" overflow="wrap" %}
```nginx
server {
    listen 80;
}
```
{% endcode %}
```

Use titled code blocks when the filename matters (config files, scripts). Plain code blocks are fine for one-liner commands.

### When to Use Which Block

| Block | Use When | Don't Use When |
|---|---|---|
| **Hints** | Warnings, prerequisites, tips, success confirmations | Every other paragraph — overuse dilutes impact |
| **Tabs** | Same task has parallel alternatives (npm vs yarn, VPS vs shared hosting) | Steps that must be done in sequence — use steppers |
| **Steppers** | Multi-step procedure where order matters (setup wizard, deploy flow) | Unordered options or comparisons — use tabs |
| **Expandable** | Supplementary detail most readers can skip | Critical information the reader needs |
| **Cards** | Landing/overview pages linking to 3+ child pages with descriptions | Inline navigation within a guide |
| **Titled code** | Config files, scripts where the filename matters | Short one-liner commands |
| **Columns** | Side-by-side comparison (code vs output, text beside image) | Long content unreadable in narrow column |
| **Buttons** | Primary CTAs on landing pages | Body of a guide — use regular links |
| **Embeds** | External media (YouTube, Figma, CodeSandbox) | Internal page links |

### Hints (Callouts)

```markdown
{% hint style="info" %}
Useful information the reader should know.
{% endhint %}
```

Styles: `info` (tips/context), `warning` (could go wrong), `danger` (will break things), `success` (step complete).

### Tabs

Use for parallel alternatives where the reader picks one path:

```markdown
{% tabs %}
{% tab title="npm" %}
```bash
npm install package
```
{% endtab %}
{% tab title="yarn" %}
```bash
yarn add package
```
{% endtab %}
{% endtabs %}
```

Good for: package managers, OS-specific commands, VPS vs shared hosting, different frameworks.

### Steppers (Numbered Steps)

Use for sequential procedures where order matters:

```markdown
{% stepper %}
{% step %}
#### Step title
Step content here.
{% endstep %}
{% step %}
#### Next step
More content.
{% endstep %}
{% endstepper %}
```

Good for: deploy flows, onboarding wizards, "what's next" progressions, grouped checklists.

### Expandable Sections

Use for supplementary detail most readers can skip:

```markdown
<details>
<summary>Click to expand</summary>

Hidden content goes here.

</details>
```

Good for: algorithm comparisons, "what each option does", verbose output, edge-case notes.

### Cards (Visual Navigation)

Use on landing/overview pages to link to child pages with visual tiles:

```html
<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody>
<tr><td><strong>Card Title</strong></td><td>Description</td><td><a href="page.md">page.md</a></td></tr>
</tbody></table>
```

Add `data-card-size="large"` on the `<table>` for wider cards.

### Columns (Side-by-Side)

```markdown
{% columns %}
{% column %}
Left column content.
{% endcolumn %}
{% column %}
Right column content.
{% endcolumn %}
{% endcolumns %}
```

### Embeds

```markdown
{% embed url="https://www.youtube.com/watch?v=abc123" %}
```

### Buttons

Use for primary CTAs on landing pages only:

```markdown
<a href="getting-started.md" class="button primary">Get Started</a>
<a href="api-reference.md" class="button secondary">API Reference</a>
```

Add `data-icon="rocket-launch"` for a FontAwesome icon prefix.

### Images (with captions)

Standard markdown works, but for captioned images:

```html
<figure><img src="path/to/image.png" alt="Alt text"><figcaption>Caption here</figcaption></figure>
```

Store space-specific images in a `.gitbook/assets/` subfolder within the space root.

### Math & TeX (KaTeX)

Block equation: `$$f(x) = x \cdot e^{2 \pi i \xi x}$$`

Inline equation: `$a^2 + b^2 = c^2$`

GitBook uses KaTeX — see [supported functions](https://katex.org/docs/supported.html).

### Annotations (Footnotes)

```markdown
GitBook supports annotations[^1] that readers can hover to read.

[^1]: This is the annotation text that appears on hover.
```

### Drawings (Excalidraw)

GitBook has built-in Excalidraw support. Press `/` → Drawing in the GitBook editor. Stored as `.drawing.svg` files. Can only be created in the GitBook UI, not via Git.

### OpenAPI Blocks

For product docs with API references, GitBook can render OpenAPI 3.0/3.1 specs. Upload a spec file or link to a hosted URL. Most relevant for `ZajProjects/` product spaces.

> [!TIP]
> **Dual-format compatibility:** Files in `ZajDocs/` are consumed by both Obsidian and GitBook. GitBook-specific `{% %}` blocks render only in GitBook; in Obsidian they appear as raw text — this is acceptable. Use `{% hint %}` for GitBook-published files; use `> [!NOTE]` only for files that will NOT be published to GitBook.

---

## Step 9 — Commit and Verify

After creating all config files:

```powershell
cd "C:\Zajaly\ZajalyDocs"
git add .
git commit -m "Add SUMMARY.md and structure for all GitBook spaces"
git push origin main
```

Then verify in GitBook:
- [ ] Each Space shows imported content from the correct subfolder
- [ ] Sidebar navigation matches your SUMMARY.md
- [ ] Home page (README.md) renders correctly
- [ ] `description` frontmatter appears in page metadata / link previews
- [ ] Each Docs Site is accessible at its `zajaly.gitbook.io/[slug]` URL
- [ ] GitBook-specific blocks (`{% hint %}`, `{% tabs %}`, etc.) render correctly
- [ ] No wikilinks (`[[...]]`) — all links use `[text](path.md)` format
- [ ] Editing a file in VS Code → push → change appears in GitBook within ~1 min
- [ ] Editing in GitBook → commit appears in GitHub within ~1 min

---

## Free Tier Limits (Reference)

| Feature | Free | Paid (from $65/site/mo) |
|---|---|---|
| Spaces | ✅ Unlimited | ✅ Unlimited |
| Public Docs Sites | ✅ Unlimited | ✅ Unlimited |
| `*.gitbook.io` subdomain | ✅ Free | ✅ Included |
| Custom domain | ❌ | ✅ Premium+ |
| Git sync (bidirectional) | ✅ Free | ✅ Free |
| `.gitbook.yaml` config | ✅ Free | ✅ Free |
| Monorepo (multi-space, one repo) | ✅ Free | ✅ Free |
| 1 editor | ✅ Free | ✅ Free |
| Multiple editors | ❌ | ✅ Paid user plans |
| Password protection | ❌ | ✅ Ultimate ($249/site/mo) |
| AI assistant for readers | ❌ | ✅ Premium+ |
| Site sections (multi-space → 1 site) | ❌ | ✅ Ultimate |
| Analytics integrations (Fathom, Plausible) | ✅ Free | ✅ Free |
| Chat widgets (Crisp) | ✅ Free | ✅ Free |
| Embeds (Figma, Arcade, Guideflow) | ✅ Free | ✅ Free |
| Auth integrations (Auth0, Okta, OIDC) | ❌ Ultimate only | ✅ Ultimate |

### Integrations Available on Free Tier

These work on free — no GitBook plan restriction (may need their own accounts):

| Category | Integrations |
|---|---|
| **Analytics** | Ahrefs, Amplitude, Fathom, Plausible |
| **Chat widgets** | Crisp, Freshdesk, Front |
| **Git Sync** | GitHub, GitLab |
| **Embeds** | Figma, GitHub Files, Arcade, Guideflow, Storylane |
| **Marketing** | Formspree, Mailchimp |

---

## Password Protection — Workarounds (Free)

GitBook's native password protection requires **Ultimate plan ($249/site/mo)**. Not worth it.

### Option A — GitBook Unlisted Links (Simplest)
- Instead of publishing publicly, use **unlisted** visibility
- Not indexed by Google, not discoverable
- Anyone with the link can view — hidden but not password-protected
- GitBook → Docs Site Settings → **Audience** → **Unlisted**

### Option B — Cloudflare Zero Trust (Free, 50 users)
Only works if you have a **custom domain** (requires upgrading GitBook to $65/mo).
- Cloudflare Zero Trust free → up to 50 users
- Email-based authentication (sends a one-time PIN to approved email addresses)
- Covers the entire domain or subdomain

### Option C — Export → Cloudflare Pages + Workers (Free, No GitBook Upgrade Needed)
Best free option that gives actual password protection:
1. GitBook syncs to GitHub (your markdown files are already there)
2. Deploy those markdown files as a static site on **Cloudflare Pages** (free, `*.pages.dev` domain)
3. Add a Cloudflare Worker for HTTP Basic Auth password protection
4. Result: password-protected static docs site at no cost

> [!NOTE]
> For now, the simplest approach: keep internal ZajalyDocs space **Unlisted** (share link only) and make product docs (Custojo, Waraq) **Public**. Revisit password protection when the need is concrete.

---

## Optional — Private ZajalyDocs via Cloudflare Worker Proxy

> Skip this for now. Come back when you want the internal ZajalyDocs space password-protected without paying $249/mo.

Since `zajaly.dev` DNS is on Cloudflare, you can route a subdomain through a Cloudflare Worker that proxies GitBook content and adds an authentication gate.

**Flow:**
```
vault.zajaly.dev → Cloudflare Worker → fetches zajaly.gitbook.io/docs → serves content
                                      + Cloudflare Zero Trust login gate (free, up to 50 users)
```

**Steps (when ready):**
1. Cloudflare Dashboard → **Workers & Pages** → **Create Worker**
2. Write a reverse proxy script that fetches from `zajaly.gitbook.io/docs`, strips headers, returns content
3. Worker → **Settings** → **Triggers** → add route: `vault.zajaly.dev/*`
4. In Cloudflare DNS: add `A` record for `vault`:
   - IP: `192.0.2.1` (this is a dummy/placeholder IP — the Worker intercepts all traffic before it reaches this address)
   - Proxy: **ON** (orange cloud ✅ — required for Worker routing)
5. **Cloudflare Zero Trust** (one.dash.cloudflare.com) → **Access** → **Applications** → **Add**
   - Application type: **Self-hosted**
   - Domain: `vault.zajaly.dev`
   - Policy: allow only your email address (or a list of emails)
   - Auth method: **One-time PIN** (sends code to your email — no Auth0 needed)
6. Now `vault.zajaly.dev` prompts for email login before showing GitBook content ✅

**Cost:** $0. Cloudflare Zero Trust free = up to 50 users.

> [!CAUTION]
> GitBook's frontend JavaScript may have internal links referencing `*.gitbook.io`. Client-side navigation may break if links aren't rewritten by the Worker. Test navigation thoroughly. This is an advanced setup — skip until you actually need it.

---

## GitBook vs Obsidian Publish — When to Use Which

| | **Obsidian Publish** | **GitBook** |
|---|---|---|
| Cost | $8/mo | Free |
| Audience | Private (password) | Public |
| Content type | Personal vault notes, SOPs | Polished product/project docs |
| Source folder | `ZajDocs/` (whole vault) | `ZajDocs/` for guides+tools, `ZajProjects/[x]/` for products |
| Navigation | Graph view + sidebar | Sidebar + search |
| Edit from | Obsidian app only | GitBook UI + VS Code/Cursor + any Git client |
| Custom domain | ✅ ($8/mo includes it) | ❌ (requires $65/mo) |
| Password | ✅ (whole site) | ❌ (requires $249/mo) |
| Best for | Your private knowledge base | Public docs for users / devs |

They coexist. Obsidian Publish = private vault with password. GitBook = public-facing documentation.

---

## Troubleshooting

### Problem: New file in repo doesn't appear in GitBook sidebar
**Cause:** File not listed in `SUMMARY.md`.
**Fix:** Add the file path to `SUMMARY.md`, commit, push. GitBook will pick it up on next sync.

### Problem: GitBook created unexpected files in my repo
**Cause:** Editing in GitBook UI generates commits. If you created README.md through GitBook UI, it may conflict with existing files.
**Fix:** Always manage `README.md`, `SUMMARY.md`, and `.gitbook.yaml` from Git, not from the GitBook editor.

### Problem: Sync seems stuck or shows no changes
**Cause:** GitBook syncs on each push event. If the webhook didn't fire, try a manual re-sync.
**Fix:** Space → Settings → Integrations → GitHub → click **Sync** to force a manual sync.

### Problem: Two spaces showing the same content
**Cause:** Overlapping monorepo paths (e.g., one space at `/ZajDocs` and another at `/ZajDocs/Subfolder`).
**Fix:** Ensure every space points to a **non-overlapping** folder. No space's path should be a parent of another space's path. Our setup avoids this: `ZajDocs/` and `ZajProjects/Custojo/` are siblings, not nested.

### Problem: GitBook reformatted my markdown unexpectedly
**Cause:** GitBook normalizes markdown when syncing from GitBook → Git. Frontmatter, whitespace, and link formats may change.
**Fix:** If you primarily edit in VS Code/Cursor, set sync direction to **GitHub → GitBook** so Git is always source of truth. Avoid editing the same file in both GitBook UI and Git simultaneously.

### Problem: Old URL returns 404 after renaming/moving a page
**Cause:** Git creates a new file and deletes the old one — GitBook cannot detect renames, so the old URL breaks.
**Fix:** Add a `redirects:` entry in `.gitbook.yaml` mapping the old path to the new file. See Step 2D.

### Problem: Same page appears twice in the sidebar
**Cause:** The same `.md` file is listed under two different sections in `SUMMARY.md`.
**Fix:** Remove the duplicate entry. Each file can only appear once in SUMMARY.md.

### Problem: Wikilinks `[[page]]` render as raw text in GitBook
**Cause:** GitBook does not support Obsidian-style wikilinks.
**Fix:** Convert all wikilinks to relative markdown links: `[Page Title](relative/path.md)`.

### Problem: GitBook block not rendering (shows raw `{% %}` text)
**Cause:** Missing closing tag or typo in the tag name.
**Fix:** Ensure every opening `{% tag %}` has a matching `{% endtag %}`. Check for typos: `{% endhint %}`, `{% endtab %}`, `{% endtabs %}`, `{% endstep %}`, `{% endstepper %}`, etc.

### Problem: Frontmatter disappears after GitBook round-trip
**Cause:** GitBook strips unrecognized frontmatter fields when syncing GitBook → Git.
**Fix:** Keep frontmatter in Git and set sync direction to GitHub → GitBook. GitBook only actively uses `description` and `icon`; ZajalyDocs custom fields (`title`, `type`, `status`, `tags`, etc.) are preserved in Git but may be stripped if GitBook writes back.

---

## Quick Reference URLs

| Site | URL |
|---|---|
| ZajalyDocs (public guides) | `zajaly.gitbook.io/docs` |
| Custojo Docs | `zajaly.gitbook.io/custojo` |
| Waraq Docs | `zajaly.gitbook.io/waraq` |
| GitBook dashboard | `app.gitbook.com` |

---

## Checklist — Complete GitBook Setup

### Infrastructure
- [ ] GitBook account created, org name: `Zajaly`
- [ ] `.gitbook.yaml` exists in each synced folder (`ZajDocs/`, `ZajProjects/Custojo/`, `ZajProjects/Waraq/`)
- [ ] `README.md` exists in each **space root** (created in Git, not GitBook UI) — subfolder READMEs optional
- [ ] `SUMMARY.md` created in each synced folder with correct page references (no duplicate entries)
- [ ] `description` frontmatter added to space root README.md files (for SEO)
- [ ] 3 Spaces created: ZajalyDocs, Custojo, Waraq
- [ ] Git Sync connected for each Space to correct monorepo path (non-overlapping)
- [ ] Sync direction: GitHub → GitBook (Git is source of truth)
- [ ] 3 Docs Sites created and published
- [ ] URL slugs set: `/docs`, `/custojo`, `/waraq`

### Verification
- [ ] Bidirectional sync verified: edit in VS Code → appears in GitBook, and vice versa
- [ ] No wikilinks (`[[...]]`) in any GitBook-synced files — all use `[text](path.md)`
- [ ] All `{% tag %}` blocks have matching `{% endtag %}`
- [ ] All code blocks specify a language
- [ ] No broken links — every linked file exists at the referenced path

### Publishing & Integrations
- [ ] At least one free integration added (e.g., Crisp chat, Fathom analytics)
- [ ] ZajalyDocs visibility set to **Unlisted** (private-ish), product docs set to **Public**

---

*Related: [[04-Mintlify-Free-Setup]] | [[05-Publishing-Stack]]*
