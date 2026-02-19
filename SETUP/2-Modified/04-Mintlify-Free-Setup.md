---
title: Mintlify Free Setup — Complete Guide
type: guide
status: published
owner: Malek
tags: [setup, mintlify, publishing, docs, api]
project: general
version: 2.0
created: 2026-02-19
updated: 2026-02-19
publish: false
---

# Mintlify Free Setup — Complete Guide

> Free Hobby tier. Custom domain included. Git-based deployment. Beautiful dev docs out of the box.

---

## Why Mintlify

Mintlify is an AI-native documentation platform built for developer-facing docs: API references, SDK guides, and technical documentation. Its free tier has one killer advantage that justifies setting it up alongside GitBook: **free custom domain** — something GitBook charges $65/mo for.

**Our use case:** `docs.zajaly.dev` → polished dev-facing documentation for Zajaly's APIs, SDKs, and developer guides. This runs on a **separate GitHub repo** ([rovony/ZajalyDocs_Mintlify](https://github.com/rovony/ZajalyDocs_Mintlify)) from ZajalyDocs (not a monorepo subfolder).

---

## Free Hobby Tier — What You Get

| Feature | Included? |
|---|---|
| Full platform access | ✅ |
| Custom domain (`docs.zajaly.dev`) | ✅ Free |
| Web editor (browser-based WYSIWYG) | ✅ |
| API playground (interactive endpoint testing) | ✅ |
| Custom components (MDX) | ✅ |
| LLM optimizations (llms.txt auto-generated) | ✅ |
| Git sync (auto-deploy on push) | ✅ |
| Built-in search | ✅ |
| Custom CSS and JS | ✅ |
| Third-party integrations | ✅ |
| Dashboard members | 1 editor |
| SEO optimizations | ✅ |
| Password protection | ❌ Pro ($250/mo) |
| AI Assistant (reader-facing chat) | ❌ Pro ($250/mo) |
| AI Writing Agent (auto-updates docs from code) | ❌ Pro ($250/mo) |
| Preview deployments (branch previews) | ❌ Pro ($250/mo) |
| Team collaboration (invite editors) | ❌ Pro ($250/mo) |
| Grammar/spelling checks | ❌ Pro ($250/mo) |
| Authentication (Auth0, SSO) | ❌ Enterprise |

**Pro plan:** $250/mo annual ($300/mo monthly) — 5 editors, AI features, preview deployments.
**Enterprise:** Custom pricing — SSO, RBAC, SLA, unlimited editors.

---

## Step 1 — Create Account & Project

1. Go to **https://mintlify.com/start**
2. Sign up with **GitHub** (easiest — enables Git sync)
3. Complete the onboarding:
   - Connect your GitHub account
   - When prompted, **create a new GitHub repository** — Mintlify generates it from the [mintlify/starter](https://github.com/mintlify/starter) template
   - Install the **Mintlify GitHub App** (enables auto-deploy on push)
4. After onboarding, your site deploys automatically to: `https://zajalydocs-mintlify.mintlify.app`

> [!TIP]
> You can skip connecting GitHub during onboarding — Mintlify creates a private repo for you. But since we want Git-based workflow, connect your own repo from the start.

### Repository Created

We created **[rovony/ZajalyDocs_Mintlify](https://github.com/rovony/ZajalyDocs_Mintlify)** during Mintlify onboarding. It was auto-generated from the Mintlify starter kit and includes:

```
ZajalyDocs_Mintlify/
├── docs.json              ← Central config (already has tabs, groups, navbar, footer)
├── index.mdx              ← Home page (starter template)
├── quickstart.mdx         ← Getting started (starter template)
├── development.mdx        ← Local dev instructions
├── essentials/            ← Guides on settings, navigation, markdown, code, images, snippets
├── api-reference/         ← API docs with example endpoints
├── ai-tools/              ← Cursor, Claude Code, Windsurf setup guides
├── snippets/              ← Reusable content snippets
├── images/                ← Static assets
├── logo/                  ← Brand logos (light.svg + dark.svg)
├── favicon.svg
├── AGENTS.md              ← AI agent instructions for the repo
├── .mintignore            ← Files to exclude from Mintlify processing
└── README.md              ← Repo readme (not published)
```

### Repository Strategy

Mintlify docs live in a **separate repo** from ZajalyDocs. This is intentional:

| Repo | Purpose | Platform |
|---|---|---|
| `rovony/ZajalyDocs` | Obsidian vault + GitBook sync | GitBook |
| `rovony/ZajalyDocs_Mintlify` | Mintlify-specific MDX + `docs.json` | Mintlify |

They serve different audiences. ZajalyDocs is your knowledge base. Mintlify is your public-facing developer docs.

> [!NOTE]
> Content flows one-way: **ZajalyDocs → ZajalyDocs_Mintlify**. When a guide in ZajalyDocs is ready for public consumption, manually adapt it as an MDX page in the Mintlify repo. Don't auto-sync — the formats (Markdown+GitBook vs MDX+components) and audiences differ.

---

## Step 2 — Clone & Set Up Locally

```powershell
cd "C:\Zajaly\Projects"
git clone https://github.com/rovony/ZajalyDocs_Mintlify.git
cd ZajalyDocs_Mintlify
```

### Install the Mintlify CLI

**Prerequisite:** Node.js v20.17.0+ (LTS recommended).

```powershell
npm install -g mint
```

### Run local preview

```powershell
mint dev
```

Preview at **http://localhost:3000**. Live-reloads as you edit files.

> [!NOTE]
> If `mint dev` fails, run `mint update` to ensure you have the latest CLI version. Make sure you're running from the directory containing `docs.json`.

### Custom port

```powershell
mint dev --port 3333
```

If the port is in use, the CLI auto-selects the next available port.

### Additional CLI Commands

| Command | Purpose |
|---|---|
| `mint update` | Update CLI to latest version |
| `mint new [dir]` | Scaffold a new project from starter kit |
| `mint broken-links` | Find broken internal links |
| `mint a11y` | Check accessibility (contrast, missing alt text) |
| `mint validate` | Validate build in strict mode (for CI/CD) |
| `mint openapi-check <file>` | Validate an OpenAPI spec file or URL |
| `mint rename <old> <new>` | Rename file and update all references |
| `mint migrate-mdx` | Convert MDX endpoint pages to OpenAPI auto-generated pages |
| `mint upgrade` | Convert deprecated `mint.json` to `docs.json` |

> [!TIP]
> Use `npx mint dev` for one-time use without installing the CLI globally.

---

## Step 3 — Project Structure

The Mintlify starter kit generated the following structure in `rovony/ZajalyDocs_Mintlify`:

```
ZajalyDocs_Mintlify/
├── docs.json              ← Central config (navigation, theme, settings)
├── index.mdx              ← Home page
├── quickstart.mdx         ← Getting started guide
├── development.mdx        ← Local dev instructions
├── essentials/             ← Guides (settings, navigation, markdown, code, images, snippets)
│   ├── settings.mdx
│   ├── navigation.mdx
│   ├── markdown.mdx
│   ├── code.mdx
│   ├── images.mdx
│   └── reusable-snippets.mdx
├── api-reference/          ← API docs
│   ├── introduction.mdx
│   └── endpoint/
│       ├── get.mdx
│       ├── create.mdx
│       ├── delete.mdx
│       └── webhook.mdx
├── ai-tools/               ← AI tool setup guides (Cursor, Claude Code, Windsurf)
├── images/                 ← Static assets
├── logo/                   ← Brand logos (light.svg + dark.svg)
├── snippets/               ← Reusable content snippets
├── favicon.svg
├── AGENTS.md               ← AI agent instructions for the repo
├── .mintignore             ← Files to exclude from processing
└── README.md               ← Repo readme (not published)
```

**Key files:**
- `docs.json` — controls everything: navigation, theme, colors, integrations
- `*.mdx` files — your content pages (Markdown + JSX components)
- `AGENTS.md` — instructions for AI coding agents working in this repo
- `.mintignore` — files to exclude from Mintlify processing (like `.gitignore`)

---

## Step 4 — Configure `docs.json`

> **Important:** Mintlify migrated from `mint.json` to `docs.json` in February 2025. If you see `mint.json` in old tutorials, it's outdated. Use `docs.json`.

The starter kit generates a working `docs.json`. Customize it for Zajaly:

```json
{
  "$schema": "https://mintlify.com/docs.json",
  "theme": "mint",
  "name": "Zajaly Developer Docs",
  "description": "Developer documentation for Zajaly APIs, SDKs, and tools.",
  "logo": {
    "light": "/logo/light.svg",
    "dark": "/logo/dark.svg"
  },
  "favicon": "/favicon.svg",
  "colors": {
    "primary": "#0A84FF",
    "light": "#4DA6FF",
    "dark": "#0066CC"
  },
  "navigation": {
    "tabs": [
      {
        "tab": "Guides",
        "groups": [
          {
            "group": "Getting Started",
            "pages": ["index", "quickstart", "development"]
          },
          {
            "group": "Core Concepts",
            "pages": [
              "essentials/settings",
              "essentials/navigation",
              "essentials/markdown",
              "essentials/code"
            ]
          }
        ]
      },
      {
        "tab": "API Reference",
        "groups": [
          {
            "group": "Overview",
            "pages": ["api-reference/introduction"]
          },
          {
            "group": "Endpoints",
            "pages": [
              "api-reference/endpoint/get",
              "api-reference/endpoint/create",
              "api-reference/endpoint/delete",
              "api-reference/endpoint/webhook"
            ]
          }
        ]
      }
    ],
    "global": {
      "anchors": [
        { "anchor": "GitHub", "href": "https://github.com/rovony", "icon": "github" }
      ]
    }
  },
  "navbar": {
    "links": [
      { "type": "github", "href": "https://github.com/rovony/ZajalyDocs_Mintlify" }
    ],
    "primary": {
      "type": "button",
      "label": "Get Started",
      "href": "https://app.zajaly.dev"
    }
  },
  "contextual": {
    "options": ["copy", "view", "chatgpt", "claude", "cursor", "mcp"]
  },
  "footer": {
    "socials": {
      "github": "https://github.com/rovony",
      "x": "https://x.com/zajaly"
    }
  }
}
```

> [!IMPORTANT]
> The `theme` field is **required** since the `docs.json` migration. Valid themes: `mint`, `maple`, `palm`, `willow`, `linden`, `almond`, `aspen`, `sequoia`.

### Navigation Structure (docs.json)

The `navigation` field is an **object** (not an array). You can nest tabs, groups, and pages:

- **`tabs`** — top-level navigation tabs (appear in header)
- **`groups`** — sidebar section headings
- **`pages`** — array of page file paths (without `.mdx` extension)
- **`anchors`** — persistent sidebar links (external or internal)
- **`dropdowns`** — expandable sidebar menus for multi-section navigation
- **`products`** — product switcher for multi-product docs

Tabs and groups are not tied to folder names — you can mix files from different folders into any tab or group.

### Additional docs.json Features

| Feature | Purpose | Example |
|---|---|---|
| `redirects` | Handle renamed/moved pages | `[{ "source": "/old", "destination": "/new" }]` |
| `banner` | Site-wide announcement | `{ "content": "v2 is live!", "dismissible": true }` |
| `appearance` | Dark/light mode toggle | `{ "default": "system", "strict": false }` |
| `contextual` | AI menu (copy, ChatGPT, Claude, Cursor) | `{ "options": ["copy", "chatgpt", "cursor"] }` |
| `seo` | Meta tags and indexing control | `{ "indexing": "navigable" }` |
| `api` | API playground settings | `{ "playground": { "display": "interactive" } }` |
| `integrations` | Analytics (GA4, PostHog, Plausible, etc.) | `{ "ga4": { "measurementId": "G-XXX" } }` |

---

## Step 5 — Write Content (MDX)

Mintlify uses MDX — Markdown with JSX components. Write normal Markdown, and add interactive components where needed.

### Basic Page Structure

```mdx
---
title: "Getting Started"
description: "Set up Custojo CRM in under 5 minutes"
---

# Getting Started

Welcome to Custojo! Follow these steps to get your CRM running.

<Steps>
  <Step title="Create an account">
    Go to [custojo.com](https://custojo.com) and sign up.
  </Step>
  <Step title="Add your first contact">
    Navigate to **Contacts → Add New** and fill in the details.
  </Step>
  <Step title="Set up a pipeline">
    Go to **Pipelines → Create** and define your sales stages.
  </Step>
</Steps>
```

### Useful Built-in Components

| Component | What it does |
|---|---|
| `<Steps>` / `<Step>` | Numbered step-by-step instructions |
| `<Card>` | Clickable card with title, icon, and description |
| `<Columns>` | Grid layout for cards or side-by-side content |
| `<Tabs>` / `<Tab>` | Tabbed content (e.g., different languages or platforms) |
| `<Accordion>` / `<AccordionGroup>` | Collapsible content sections |
| `<Note>` `<Tip>` `<Warning>` `<Info>` `<Check>` `<Danger>` | Callout banners (six built-in styles) |
| `<CodeGroup>` | Code in multiple languages with synced tabs |
| `<ResponseField>` / `<Expandable>` | API response field documentation (nestable) |
| `<ParamField>` | API parameter documentation (path, body, query, header) |
| `<RequestExample>` / `<ResponseExample>` | API request/response examples in sidebar |
| `<Frame>` | Images with captions and visual framing |
| `<Tooltip>` | Inline hover definitions |
| `<Badge>` | Inline status labels ("NEW", "BETA") |
| `<Prompt>` | Copyable AI prompts with Cursor integration |
| `<Update>` | Changelog entries with version labels |
| Mermaid | Flowcharts and diagrams via ` ```mermaid ` code blocks |

### Code Examples with Tabs

````mdx
<CodeGroup>
```bash cURL
curl -X POST https://api.custojo.com/contacts \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{"name": "John Doe", "email": "john@example.com"}'
```

```python Python
import requests

response = requests.post(
    "https://api.custojo.com/contacts",
    headers={"Authorization": "Bearer YOUR_API_KEY"},
    json={"name": "John Doe", "email": "john@example.com"}
)
```

```javascript Node.js
const response = await fetch("https://api.custojo.com/contacts", {
  method: "POST",
  headers: {
    "Authorization": "Bearer YOUR_API_KEY",
    "Content-Type": "application/json"
  },
  body: JSON.stringify({ name: "John Doe", email: "john@example.com" })
});
```
</CodeGroup>
````

---

## Step 6 — API Reference (OpenAPI)

If your SaaS products have APIs, Mintlify can auto-generate interactive API docs from an OpenAPI spec.

### 6A — Add Your OpenAPI Spec

Place your OpenAPI 3.0+ spec file in the repo:

```
api-reference/openapi.json
```

Or reference a URL in `docs.json`:

```json
{
  "openapi": "https://api.custojo.com/openapi.json"
}
```

### 6B — Auto-Generate Endpoint Pages

```powershell
npx @mintlify/scraping@latest openapi-file ./api-reference/openapi.json -o ./api-reference
```

This generates one `.mdx` file per endpoint, organized by tag/group.

### 6C — API Playground

Mintlify's API Playground lets readers test your API directly in the docs. Configure in `docs.json`:

```json
{
  "api": {
    "openapi": "api-reference/openapi.json",
    "playground": {
      "display": "interactive"
    },
    "examples": {
      "languages": ["bash", "javascript", "python"]
    },
    "mdx": {
      "auth": { "method": "bearer" },
      "server": "https://api.custojo.com"
    }
  }
}
```

Playground `display` options: `interactive` (default — users can make live requests), `simple` (read-only examples), `none` (no playground).

Readers can input their API key and make live requests from the docs page.

---

## Step 7 — Custom Domain (`docs.zajaly.dev`)

This is the main reason to use Mintlify on free tier — custom domain at $0.

### 7A — Configure in Mintlify Dashboard

1. Go to **https://dashboard.mintlify.com**
2. Select your project → **Settings** → **Domain Setup**
3. Enter: `docs.zajaly.dev`

### 7B — Configure Cloudflare DNS

In Cloudflare DNS for `zajaly.dev`:

| Type | Name | Target | Proxy |
|---|---|---|---|
| CNAME | `docs` | `cname.mintlify-dns.com` | **DNS only** (gray cloud) |

### 7C — Cloudflare-Specific Settings (CRITICAL)

Mintlify uses Let's Encrypt for SSL certificates. Cloudflare can interfere if not configured correctly:

1. **SSL/TLS → Overview → Encryption mode:** Set to **Full (strict)**
2. **SSL/TLS → Edge Certificates → Always Use HTTPS:** **Disable** this
3. **Do NOT redirect** the `/.well-known/acme-challenge` path (used for certificate validation)

> [!CAUTION]
> If "Always Use HTTPS" is enabled in Cloudflare, Let's Encrypt cannot validate your domain and certificate provisioning will fail. This is the #1 reason Mintlify custom domains fail on Cloudflare.

### 7D — SEO and Appearance

Add to `docs.json`:

```json
{
  "seo": {
    "metatags": {
      "og:site_name": "Zajaly Developer Docs"
    },
    "indexing": "navigable"
  },
  "appearance": {
    "default": "dark",
    "strict": false
  }
}
```

- `seo.indexing`: `navigable` (only pages in navigation) or `all` (every page)
- `appearance.default`: `system`, `light`, or `dark`
- `appearance.strict`: `true` hides the dark/light mode toggle

### 7E — Wait & Verify

DNS propagation takes 15 min to 48 hours (usually under 1 hour). Once propagated, `docs.zajaly.dev` serves your Mintlify docs with SSL.

---

## Step 8 — Deploy

Mintlify auto-deploys on every push to your default branch. No build commands needed.

```powershell
cd "C:\Zajaly\Projects\ZajalyDocs_Mintlify"
git add .
git commit -m "Customize docs for Zajaly"
git push origin main
```

Monitor deployment status:
- **Mintlify Dashboard → Overview** — shows deployment status
- **GitHub Actions** — Mintlify GitHub App triggers on push

Your docs are live at `docs.zajaly.dev` (or `zajalydocs-mintlify.mintlify.app` before custom domain is set up).

---

## Step 9 — Editing Workflows

### Code-Based (VS Code / Cursor)

1. Edit `.mdx` files locally
2. Run `mint dev` for live preview at localhost:3000
3. Push to GitHub → auto-deploys to production

Best for: major restructuring, bulk edits, new pages, API doc generation.

### Web Editor (Browser)

1. Go to **dashboard.mintlify.com** → your project
2. Switch between **Visual** and **Markdown** editing modes
3. Use **drag-and-drop** to reorganize navigation without editing `docs.json`
4. Create **shareable preview links** for team review
5. Click **Publish** → instantly deployed

Key features:
- **Live preview** — see changes in real-time without creating a deploy
- **Git synchronization** — all changes sync automatically with your repo
- **Branch workflows** — create branches for team collaboration (Pro)

Best for: quick typo fixes, content tweaks, navigation reorganization.

### Mintlify Agent (Pro — Slack or API)

Prompt the agent via Slack (`@mintlify`) or the API:

- `@mintlify Update docs for this PR: [link]` — auto-update docs from code changes
- `@mintlify Generate release notes for this PR: [link]` — changelog from commits
- `@mintlify Review the API rate limiting section` — content review
- `@mintlify Add this diagram to the architecture page` (attach image)
- API: `POST /api/agent/jobs` for CI/CD automation (`asDraft: false` for auto-merge)

Best for: keeping docs in sync with code, automated updates, review cycles.

### All Together

All three methods commit to the same Git repo (`rovony/ZajalyDocs_Mintlify`). Use code-based for heavy work, web editor for light edits, agent for automation.

### Content Sync: ZajalyDocs → Mintlify

The two repos serve different purposes and formats:

| | ZajalyDocs (`rovony/ZajalyDocs`) | Mintlify (`rovony/ZajalyDocs_Mintlify`) |
|---|---|---|
| Format | Markdown + GitBook `{% %}` blocks | MDX + JSX `<Component>` tags |
| Audience | Internal knowledge base | Public developer docs |
| Links | `[[wikilinks]]` | `/relative-paths` |
| Platform | GitBook + Obsidian | Mintlify |

**Sync is manual and one-way: ZajalyDocs → Mintlify.** When adapting content:

1. Copy the guide text from ZajalyDocs
2. Convert `[[wikilinks]]` to `[text](/path)` format
3. Replace GitBook blocks with Mintlify components:
   - `{% hint %}` → `<Note>` / `<Warning>` / `<Tip>`
   - `{% tabs %}` → `<Tabs>` / `<Tab>`
   - `{% stepper %}` → `<Steps>` / `<Step>`
   - `{% code %}` → fenced code blocks with filename
4. Add MDX frontmatter (`title`, `description`)
5. Add the page to `docs.json` navigation
6. Test with `mint dev`

> [!TIP]
> Don't sync everything. Only publish developer-facing content (API guides, SDK docs, getting started) to Mintlify. Internal SOPs and knowledge base content stays in ZajalyDocs/GitBook.

---

## Step 10 — Per-Product Docs Strategy

You can create **multiple Mintlify projects** (each on its own subdomain) or use **tabs** within one project:

### Option A — One Project, Multiple Tabs (simpler)

```json
{
  "navigation": {
    "tabs": [
      {
        "tab": "General",
        "pages": ["index", "quickstart"]
      },
      {
        "tab": "Custojo API",
        "groups": [
          { "group": "Getting Started", "pages": ["custojo/overview", "custojo/auth"] }
        ]
      },
      {
        "tab": "Waraq API",
        "groups": [
          { "group": "Getting Started", "pages": ["waraq/overview", "waraq/sdk"] }
        ]
      }
    ]
  }
}
```

All at `docs.zajaly.dev` with tabs for each product.

### Option A-2 — One Project, Products Switcher (best for many products)

```json
{
  "navigation": {
    "products": [
      {
        "product": "Custojo",
        "icon": "users",
        "groups": [
          { "group": "Getting Started", "pages": ["custojo/overview"] },
          { "group": "API", "pages": ["custojo/api/users"] }
        ]
      },
      {
        "product": "Waraq",
        "icon": "code",
        "pages": ["waraq/overview"]
      }
    ]
  }
}
```

Products appear as a dropdown switcher. Start with tabs, upgrade to products when you have 3+.

### Option B — Separate Projects Per Product

- `docs.zajaly.dev` → General Zajaly dev docs (`rovony/ZajalyDocs_Mintlify`)
- `docs.custojo.com` → Custojo API docs (separate Mintlify project + repo)
- `docs.waraq.dev` → Waraq API docs (separate Mintlify project + repo)

Each gets its own free custom domain. Start with Option A, split later when products grow.

---

## Troubleshooting

### `mint dev` fails with "docs.json not found"
**Fix:** Run the command from the directory containing `docs.json`. If you have `mint.json` instead, run `mint upgrade` to auto-convert it (Mintlify migrated to `docs.json` in early 2025).

### `mint dev` fails with "Could not load the 'sharp' module"
**Fix:** Uninstall the CLI (`npm uninstall -g mint`), upgrade to Node.js v20.17.0+, then reinstall (`npm install -g mint`).

### Custom domain shows SSL error
**Fix:** In Cloudflare: SSL mode → Full (strict). Disable "Always Use HTTPS" in Edge Certificates. Wait 30 min. Do NOT redirect `/.well-known/acme-challenge` (used for Let's Encrypt validation).

### Pages return 404 in browser
**Fix:** Ensure every page is listed in `docs.json` → `navigation`. Pages not listed return 404 even if the file exists. If you renamed a page, add a `redirects` entry in `docs.json`.

### Deployment stuck or failed
**Fix:** Check the Mintlify Dashboard → Overview for deployment status. Run `mint update` locally to get latest CLI. Run `mint validate` to check for build errors. Verify `docs.json` is valid JSON (no trailing commas).

### API Playground not showing
**Fix:** Ensure `openapi.json` is valid OpenAPI 3.0+ (`mint openapi-check ./openapi.json`). Check that `api.playground.display` is not set to `none` in `docs.json`.

### Components not rendering (raw JSX tags showing)
**Fix:** Ensure the file uses `.mdx` extension (not `.md`). Check that every opening `<Component>` has a matching `</Component>`. Component names are PascalCase.

### Local preview doesn't match production
**Fix:** Run `mint update` to get the latest CLI version. Clear `~/.mintlify` folder and run `mint dev` again.

### Broken internal links
**Fix:** Run `mint broken-links` to find all broken links. Use `--check-anchors` to also check `#anchor` links. Use `/path` format without `.mdx` extension.

### `mint.json` vs `docs.json` conflict
**Fix:** If both files exist, delete `mint.json` and use only `docs.json`. Run `mint upgrade` to convert automatically.

### Client version shows 'none' after installation
**Fix:** Corporate firewall or VPN may block `releases.mintlify.com`. Ask IT to whitelist this domain.

---

## Checklist — Complete Mintlify Setup

### Infrastructure
- [ ] Account created at mintlify.com (GitHub sign-in)
- [ ] GitHub repo `rovony/ZajalyDocs_Mintlify` connected with Mintlify GitHub App
- [ ] `docs.json` configured with `theme`, `name`, `colors.primary`, `navigation`
- [ ] Logos (`/logo/light.png`, `/logo/dark.png`) and favicon (`/favicon.svg`) in place

### Local Development
- [ ] Node.js v20.17.0+ installed
- [ ] CLI installed (`npm i -g mint`)
- [ ] `mint dev` works locally at localhost:3000
- [ ] `mint validate` passes with no errors

### Custom Domain
- [ ] Custom domain `docs.zajaly.dev` set in Dashboard → Settings → Domain Setup
- [ ] Cloudflare CNAME: `docs` → `cname.mintlify-dns.com` (DNS only, gray cloud)
- [ ] Cloudflare SSL: Full (strict) mode, "Always Use HTTPS" disabled
- [ ] Site accessible at `docs.zajaly.dev` with valid SSL

### Content & Verification
- [ ] Pushed to GitHub → auto-deployed
- [ ] All pages have `title` and `description` frontmatter
- [ ] No wikilinks (`[[...]]`) in any `.mdx` file
- [ ] `mint broken-links` reports no broken links
- [ ] `mint a11y` reports no accessibility issues
- [ ] At least one API endpoint documented with OpenAPI playground working
- [ ] Navigation matches `docs.json` (no orphaned pages)

---

## Quick Reference

| Item | Value |
|---|---|
| Dashboard | `dashboard.mintlify.com` |
| Web Editor | `dashboard.mintlify.com` → Edit |
| Default URL | `zajalydocs-mintlify.mintlify.app` |
| Custom domain | `docs.zajaly.dev` |
| Config file | `docs.json` (NOT `mint.json`) |
| Required theme | One of: `mint`, `maple`, `palm`, `willow`, `linden`, `almond`, `aspen`, `sequoia` |
| CLI commands | `mint dev` / `mint update` / `mint validate` / `mint broken-links` / `mint a11y` |
| CNAME target | `cname.mintlify-dns.com` |
| Node.js required | v20.17.0+ (LTS) |
| Local repo | `C:\Zajaly\Projects\ZajalyDocs_Mintlify` |
| GitHub repo | `rovony/ZajalyDocs_Mintlify` |

---

*Related: [[03-GitBook-Free-Setup]] | [[05-Publishing-Stack]]*
*Save to: C:\Zajaly\ZajalyDocs\_Admin\Setup\04-Mintlify-Free-Setup.md*
*Version: 2.0 — February 19, 2026*
