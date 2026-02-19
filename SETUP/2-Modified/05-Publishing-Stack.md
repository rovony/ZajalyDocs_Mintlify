---
title: Publishing Stack — Complete Setup Guide
type: guide
status: published
owner: Malek
tags: [setup, publishing, hashnode, featurebase, blog, changelog, domain]
project: general
version: 1.0
created: 2026-02-19
updated: 2026-02-19
publish: false
---

# Publishing Stack — Complete Setup Guide

> Free tools for help docs, changelog, feedback, and blog — all with custom domains. Total cost: $0.

---

## The Goal

Every SaaS product needs three public-facing content channels:
1. **Help docs** — product documentation for customers
2. **Changelog** — what's new, what changed
3. **Blog** — articles, tutorials, thought leadership

Our stack achieves all three at $0/mo using custom domains.

---

## Tool Assignments

| Channel | Tool | Custom Domain? | Cost |
|---|---|---|---|
| Help docs (dev-facing) | Mintlify | ✅ `docs.zajaly.dev` | Free |
| Help docs (per product) | GitBook | ❌ `zajaly.gitbook.io/[product]` | Free |
| Changelog + Feedback | Featurebase | ✅ `changelog.zajaly.dev` | Free |
| Blog | Hashnode | ✅ `blog.zajaly.dev` | Free |
| Private knowledge base | Obsidian Publish | ✅ `vault.zajaly.dev` | $8/mo |
| Courses | Skillplate | ✅ `learn.zajaly.dev` | Lifetime |

---

## Part A — Hashnode Blog Setup

### A1 — Create Account

1. Go to **https://hashnode.com** → **Sign up** (GitHub or email)
2. Create a **publication** → name: `Zajaly Blog`
3. Choose a Hashnode subdomain: `zajaly.hashnode.dev`

### A2 — Custom Domain (`blog.zajaly.dev`)

1. Hashnode → your publication → **Dashboard** → **Domain**
2. Enter: `blog.zajaly.dev`
3. In Cloudflare DNS for `zajaly.dev`:

| Type | Name | Target | Proxy |
|---|---|---|---|
| CNAME | `blog` | `hashnode.network` | **DNS only** (gray cloud) |

4. Back in Hashnode → click **Verify** → wait up to 30 min

### A3 — Configure Publication

- **Appearance:** Upload logo, set brand colors, choose theme
- **Newsletter:** Hashnode has built-in newsletter — readers can subscribe via email
- **SEO:** Auto-generates meta tags, Open Graph images, sitemap
- **Series:** Group related posts into series (e.g., "Laravel Deployment Series")
- **Pages:** Create static pages (About, Contact)

### A4 — Writing Workflow

Content drafts live in `ZajContent/Blog/Drafts/` in your vault. When ready:

1. Write/polish in Obsidian (markdown)
2. Copy content to Hashnode editor (or use their GitHub backup feature)
3. Hashnode publishes with full SEO, newsletter notification, and social cards

### A5 — Hashnode GitHub Backup

Hashnode can automatically back up all published posts to a GitHub repo:

1. Dashboard → **Integrations** → **GitHub Backup**
2. Connect repo (can be `rovony/zajaly-blog-backup` or a folder in any repo)
3. Every published post auto-commits as markdown to the repo

### A6 — Free Tier Highlights

| Feature | Available? |
|---|---|
| Custom domain | ✅ Free |
| Newsletter (built-in) | ✅ Free |
| SEO + Open Graph | ✅ Free |
| Series (group posts) | ✅ Free |
| Custom CSS | ✅ Free |
| Static pages | ✅ Free |
| GitHub backup | ✅ Free |
| Team blogs | ✅ Free |
| API access | ✅ Free |
| No ads on your blog | ✅ Free |

---

## Part B — Featurebase Setup (Changelog + Feedback + Roadmap)

### B1 — Create Account

1. Go to **https://featurebase.app** → **Sign up**
2. Create workspace → name: `Zajaly` (or create per-product: `Custojo`, `Waraq`)

### B2 — What You Get Free

Featurebase gives you three tools in one:

| Feature | What it does |
|---|---|
| **Changelog** | Public changelog with email notifications |
| **Feedback board** | Users submit and vote on feature requests |
| **Roadmap** | Public or private product roadmap |

### B3 — Custom Domain (`changelog.zajaly.dev`)

1. Featurebase → **Settings** → **Custom domain**
2. Enter: `changelog.zajaly.dev`
3. In Cloudflare DNS:

| Type | Name | Target | Proxy |
|---|---|---|---|
| CNAME | `changelog` | (as shown in Featurebase settings) | **DNS only** (gray cloud) |

4. Verify in Featurebase

### B4 — Per-Product Setup

You can create separate workspaces per product, each with its own changelog:

| Workspace | Custom Domain | Content |
|---|---|---|
| Zajaly (general) | `changelog.zajaly.dev` | General Zajaly updates |
| Custojo | `changelog.custojo.com` | Custojo-specific updates |
| Waraq | `changelog.waraq.dev` | Waraq-specific updates |

Or use one workspace with **boards** per product (simpler to manage).

### B5 — Changelog Writing Workflow

1. Build a feature in your SaaS product
2. Write a changelog entry in `ZajProjects/[product]/Changelog.md` (your vault)
3. Copy to Featurebase → **New Post** → select category → publish
4. Featurebase notifies subscribed users via email

### B6 — Feedback Board

Enable the feedback board so customers can:
- Submit feature requests
- Vote on existing requests
- Comment and discuss

This feeds directly into your product roadmap. Embed the board in your product with Featurebase's widget (JavaScript snippet).

### B7 — Free Tier Limits

| Feature | Free |
|---|---|
| Changelog posts | ✅ Unlimited |
| Feedback boards | ✅ 1 board |
| Roadmap | ✅ Public |
| Custom domain | ✅ |
| Email notifications | ✅ |
| Widget embed | ✅ |
| SSO | ❌ Paid |
| Multiple boards | ❌ Paid |
| Custom branding (remove Featurebase logo) | ❌ Paid |

---

## Part C — Docusaurus Alternative (If Needed Later)

If Mintlify or GitBook don't fit for a specific product's help docs, Docusaurus on Vercel is a free, fully-controlled alternative:

```powershell
npx create-docusaurus@latest custojo-help classic
cd custojo-help
npm run start
```

Deploy to Vercel:
1. Push to GitHub
2. Connect repo on vercel.com → auto-deploys
3. Add custom domain in Vercel settings (free)

**When to use:** Customer-facing help centers where you want full React control and self-hosted. Mintlify is better for API docs; GitBook is easier for non-technical docs.

---

## Part D — Per-Product Publishing Map

```
Custojo
├── Help docs  → GitBook → zajaly.gitbook.io/custojo         [ZajProjects/Custojo/]
├── Changelog  → Featurebase → changelog.custojo.com          [ZajProjects/Custojo/Changelog.md]
├── Feedback   → Featurebase (same workspace as changelog)
└── Blog       → Hashnode → blog.custojo.com (or shared)      [ZajContent/Blog/]

Waraq.dev
├── Help docs  → GitBook → zajaly.gitbook.io/waraq            [ZajProjects/Waraq/]
├── Changelog  → Featurebase → changelog.waraq.dev            [ZajProjects/Waraq/Changelog.md]
├── Feedback   → Featurebase (same workspace)
└── Blog       → Hashnode (shared or separate)                 [ZajContent/Blog/]

General / Zajaly
├── Knowledge  → Obsidian Publish → vault.zajaly.dev ($8/mo, password protected)
├── Dev docs   → Mintlify → docs.zajaly.dev (FREE)
├── Public KB  → GitBook → zajaly.gitbook.io/docs              [ZajDocs/]
├── Blog       → Hashnode → blog.zajaly.dev (FREE)             [ZajContent/Blog/]
├── Changelog  → Featurebase → changelog.zajaly.dev (FREE)
├── Courses    → Skillplate → learn.zajaly.dev (lifetime)       [ZajContent/Courses/]
```

---

## Part E — Complete DNS Records (zajaly.dev on Cloudflare)

| Subdomain | Type | Name | Target | Proxy | Service | Cost |
|---|---|---|---|---|---|---|
| `docs.zajaly.dev` | CNAME | `docs` | `cname.mintlify-dns.com` | DNS only | Mintlify | Free |
| `vault.zajaly.dev` | CNAME | `vault` | `publish-main.obsidian.md` | DNS only | Obsidian Publish | $8/mo |
| `blog.zajaly.dev` | CNAME | `blog` | `hashnode.network` | DNS only | Hashnode | Free |
| `changelog.zajaly.dev` | CNAME | `changelog` | (Featurebase target) | DNS only | Featurebase | Free |
| `learn.zajaly.dev` | CNAME | `learn` | (Skillplate target) | DNS only | Skillplate | Lifetime |

**All records:** DNS only (gray cloud). No Cloudflare proxy except where specifically required.

> [!CAUTION]
> **For Mintlify specifically:** also set Cloudflare SSL to "Full (strict)" and disable "Always Use HTTPS" in Edge Certificates. See 04-Mintlify-Free-Setup.md Step 7C.

---

## Checklist — Complete Publishing Stack

- [ ] Hashnode account created, publication named
- [ ] `blog.zajaly.dev` CNAME added and verified
- [ ] Hashnode GitHub backup connected
- [ ] Featurebase workspace created
- [ ] `changelog.zajaly.dev` CNAME added and verified
- [ ] Feedback board enabled in Featurebase
- [ ] All DNS records added in Cloudflare (see table above)
- [ ] All custom domains verified and working
- [ ] First blog post published as test
- [ ] First changelog entry published as test

---

*Related: [[03-GitBook-Free-Setup]] | [[04-Mintlify-Free-Setup]] | [[07-Skillplate-Courses]]*
*Save to: C:\Zajaly\ZajalyDocs\_Admin\Setup\05-Publishing-Stack.md*
*Version: 1.0 — February 19, 2026*
