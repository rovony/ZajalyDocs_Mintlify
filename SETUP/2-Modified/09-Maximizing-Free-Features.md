---
title: Maximizing Free Features — Complete Guide
type: guide
status: published
owner: Malek
tags: [setup, optimization, free-tier, tips]
project: general
version: 1.0
created: 2026-02-19
updated: 2026-02-19
publish: false
---

# Maximizing Free Features — Complete Guide

> Every paid and free tool in the stack has untapped capabilities. This guide covers power moves you should set up from day one.

---

## Obsidian ($4/mo Sync + $8/mo Publish)

### Sync Power Moves

- **Selective sync:** Exclude large folders (e.g., `_Sources/` with big PDFs) from Sync to save the 10 GB limit. Access those via Git instead.
- **Version history:** Obsidian Sync keeps 12 months of version history for every synced note. Use this as an undo system — go to a note → three-dot menu → **View version history** → restore any previous version.
- **Plugin sync:** Sync your plugins across devices so your phone/tablet has the exact same setup as your PC.
- **Encrypted sync:** End-to-end AES-256 encryption. Not even Obsidian can read your notes. Useful if you store client data or internal SOPs.

### Publish Power Moves

- **Dataview on published pages:** Dataview queries in published notes render as static tables. Create auto-generated index pages: "All Server Guides" with a Dataview query that lists all published server guides.
- **Custom CSS:** Publish supports custom CSS snippets. Brand your published site with your colors, fonts, and layout. Settings → Publish → **Custom CSS** → paste your styles.
- **Graph View for readers:** Enable graph view on your published site. Readers can visually explore connections between your notes — a unique navigation experience no other platform offers.
- **Backlinks display:** Show backlinks on published pages so readers discover related content they might have missed.
- **Search:** Built-in full-text search across all published notes.
- **Redirect old URLs:** If you rename published notes, set up redirects in Publish settings so old links don't break.

### Plugin Power Moves

- **Dataview auto-dashboards:** Create a Dashboard.md at vault root with queries for: recently updated, needs attention (status:draft or outdated), all published content, per-project lists.
- **Templater date automation:** Templates auto-fill `{{date}}` fields so `created` and `updated` frontmatter is always correct.
- **Tag Wrangler bulk operations:** Right-click any tag → rename it across the entire vault instantly.
- **Calendar + daily notes:** Use Calendar plugin to create daily notes for capturing ideas, meeting notes, or progress logs. Move useful content from daily notes to permanent homes during weekly processing.
- **Linter auto-formatting:** Configure Linter to auto-sort YAML frontmatter keys, add blank lines after headings, remove trailing spaces — on every save. Consistent formatting without thinking about it.

---

## GitBook (Free)

### Capabilities You Get for Free

- **Unlimited public spaces and Docs Sites** — publish as many product docs as you want
- **Full version history** — every change tracked, revertible
- **Bidirectional Git sync** — edit in VS Code AND GitBook interchangeably
- **Built-in search** — readers can search across all your docs
- **Auto-generated table of contents** — from heading structure
- **Markdown + rich blocks** — supports tables, code blocks, images, embeds
- **Comments** — collaborate with comments on any content block

### Power Moves

- **SUMMARY.md navigation control:** Manually define sidebar order. Files not in SUMMARY.md are synced but invisible — use this to keep draft files in Git without publishing them.
- **Multi-space monorepo:** All your product docs live in one Git repo with different GitBook spaces per subfolder. One push updates everything.
- **Unlisted for semi-private docs:** Set ZajalyDocs space to Unlisted — accessible only to people you share the link with.
- **Free integrations:** Crisp (live chat), Fathom/Plausible (analytics), Formspree (contact forms), Figma (design embeds), GitHub Files (inline code from repos). All free to install.
- **OpenAPI support:** GitBook can render API documentation from OpenAPI specs.

---

## Mintlify (Free Hobby Tier)

### Capabilities You Get for Free

- **Custom domain** — the flagship free feature. `docs.zajaly.dev` at $0.
- **API Playground** — readers can test your API endpoints live in the docs
- **MDX components** — Steps, Cards, Tabs, Accordions, CodeGroups, Callouts for rich docs
- **LLM optimizations** — auto-generates `llms.txt` so AI tools can discover and parse your docs
- **Custom CSS and JS** — full style control
- **SEO optimizations** — automatic meta tags, sitemap, Open Graph
- **Git-based deployment** — push to GitHub → auto-deploys in minutes
- **Web editor** — browser-based WYSIWYG for quick edits

### Power Moves

- **API Playground for every product:** If Custojo, Waraq, etc. have APIs, create OpenAPI specs and let users test live from docs.
- **MDX rich content:** Use `<Steps>`, `<CodeGroup>` (multi-language code tabs), `<Card>` grids, `<Accordion>` for FAQ sections. Makes docs feel like an app, not a text file.
- **docs.json recursive navigation:** Organize docs into tabs + groups + pages with arbitrary nesting. No folder structure constraints — you can mix files from any folder.
- **Snippets:** Create reusable content in `snippets/` folder. Reference in any page to avoid repetition (e.g., common auth instructions).

---

## Hashnode (Free)

### Everything is Free

- **Custom domain** — `blog.zajaly.dev` at $0
- **Newsletter** — built-in subscriber management and email delivery
- **Series** — group related posts into ordered series
- **API** — programmatically create/manage posts (GraphQL API)
- **GitHub backup** — all posts auto-committed to a GitHub repo
- **Custom CSS** — brand your blog
- **Static pages** — About, Contact, etc.
- **Team blog** — multiple authors
- **No ads** — Hashnode doesn't inject ads into your blog

### Power Moves

- **Series for course marketing:** Create a "Laravel Deployment" series on Hashnode that mirrors your Skillplate course. Free content on blog → upsell to paid course.
- **Newsletter for audience building:** Every blog subscriber is a potential course customer. Build your email list for free via Hashnode's built-in newsletter.
- **GitHub backup as archive:** All your published posts backed up as markdown in Git. If you ever leave Hashnode, your content is already portable.
- **SEO head start:** Hashnode auto-generates sitemap, meta tags, Open Graph images. Your posts rank on Google with zero SEO effort.

---

## Featurebase (Free)

### What's Free

- **Changelog** — unlimited posts with email notifications
- **Feedback board** — 1 board where users submit and vote on feature requests
- **Roadmap** — public view of what's planned/in-progress/done
- **Custom domain** — `changelog.zajaly.dev`
- **Widget embed** — JavaScript snippet to embed feedback board in your app

### Power Moves

- **Feedback → Roadmap loop:** Let customers vote on features. Top-voted items go on the roadmap. Ship them → announce in changelog. Customers see their input matters.
- **Embed in Custojo/Waraq:** Add the Featurebase widget to your SaaS app so customers can submit feedback without leaving the product.
- **Changelog as marketing:** Every changelog post is a chance to re-engage users. "We shipped X that you asked for" emails drive retention.

---

## Skillplate (Lifetime)

### Key Free-Forever Features

- **AI Course Builder** — generates full course structure from a topic
- **0% commission** — Stripe/PayPal fees only (no Skillplate cut)
- **Multi-language** — 22 languages, 135 currencies built-in
- **Email marketing** — built-in sequences and automations
- **Community** — Discord integration with auto access control
- **Bundles** — create product bundles from existing courses
- **Pre-sales** — sell courses before content is complete
- **AI copywriting** — generate sales page text, headlines, CTAs

### Power Moves

- **Bundle existing courses:** 10 courses → 15+ products by mixing bundles. More SKUs = more pricing options.
- **Pre-sell to validate:** Create course outline with AI → set up pre-sale page → test demand before recording all videos.
- **Multi-language courses:** Same course in EN, ES, AR triples your addressable market.
- **Discord community upsell:** Offer premium Discord access as part of a course bundle or standalone membership.

---

## Make.com (Free)

### Free Tier

- 1,000 operations/month
- 2 active scenarios
- 15-minute minimum interval

### Power Moves

- **Notion → GitHub sync:** Keep Notion collaborators in sync with your Obsidian vault without them ever touching Git.
- **Conditional routing:** Only sync files with specific tags or in specific folders.
- **Error handling:** Set up email notifications if a sync scenario fails.
- **Batch operations:** Group multiple small changes into one Git commit to save operations.

---

## Monthly Cost Summary (Maximized)

| Tool | Cost | What you get for it |
|---|---|---|
| Obsidian Sync | $4/mo | Multi-device encrypted sync, 12mo version history |
| Obsidian Publish | $8/mo | Password-protected site, custom domain, graph view |
| GitBook | Free | Unlimited public docs, Git sync, monorepo |
| Mintlify | Free | Custom domain, API playground, MDX, web editor |
| Hashnode | Free | Custom domain, newsletter, SEO, GitHub backup |
| Featurebase | Free | Changelog, feedback board, roadmap, custom domain |
| Skillplate | $0 (lifetime) | Courses, payments, email, community, AI builder |
| Make.com | Free | 1,000 ops/mo Notion ↔ GitHub sync |
| **Total** | **$12/mo** | Complete documentation + publishing + courses |

Optional additions when ready:
- Synthesia Starter: $18/mo (AI video for course lessons)
- Make.com Pro: $9/mo (10,000 ops if free tier isn't enough)

---

*Related: [[00-MASTER-SETUP-GUIDE]]*
*Save to: C:\Zajaly\ZajalyDocs\_Admin\Setup\09-Maximizing-Free-Features.md*
*Version: 1.0 — February 19, 2026*
