---
title: Password Protection — Complete Guide
type: guide
status: published
owner: Malek
tags: [setup, security, password, protection, cloudflare]
project: general
version: 1.0
created: 2026-02-19
updated: 2026-02-19
publish: false
---

# Password Protection — Complete Guide

> What you can and can't lock down across the stack, and free workarounds for tools that charge for it.

---

## Protection Summary by Platform

| Platform | Password Protection | How | Cost |
|---|---|---|---|
| **Obsidian Publish** | ✅ Entire published site | Publish settings → Password | $8/mo (included) |
| **GitBook** | ❌ Not on free tier | Requires Ultimate plan | $249/site/mo |
| **Mintlify** | ❌ Not on free tier | Requires Pro plan | $250/mo |
| **Hashnode** | ❌ No | All posts are public | N/A |
| **Featurebase** | ⚠️ Partial | Visibility per board (public/private) | Free |
| **Skillplate** | ✅ Per course | Free, paid, or invite-only courses | Included (lifetime) |
| **Cloudflare Zero Trust** | ✅ Any domain you control | Email-based one-time PIN | Free (50 users) |

---

## Obsidian Publish — Password Protection ($8/mo)

**The only affordable built-in password protection in the stack.**

### How It Works

1. In Obsidian: Publish settings → your site → **Site options** → **Password**
2. Set one password
3. All published pages are behind this password
4. Visitors see a login screen before any content loads

### Limitations

- **Site-wide only** — cannot password-protect individual pages
- **One password** — no per-user authentication
- **No user accounts** — just a shared password
- No audit log of who accessed what

### Best For

Your private knowledge base at `vault.zajaly.dev`. Share the password with team members or clients who need access to your internal guides and SOPs.

---

## GitBook — Free Tier Workarounds

### Option A — Unlisted Links (Simplest, Free)

1. GitBook → Docs Site → Settings → **Audience** → **Unlisted**
2. Site is NOT indexed by Google, NOT discoverable
3. Anyone with the link can view — hidden but not password-protected
4. Share the link only with people who need access

**Pros:** Zero effort. Free. **Cons:** Anyone who gets the link can share it.

### Option B — Cloudflare Zero Trust (Free, 50 Users)

This works ONLY if you have a custom domain pointing to your GitBook content. Since GitBook free doesn't include custom domains, you'd need the Worker proxy approach (Option C).

### Option C — Cloudflare Worker Proxy (Free, Full Password Protection)

Since `zajaly.dev` is on Cloudflare, you can route a subdomain through a Cloudflare Worker that proxies GitBook content and adds authentication.

**Flow:**
```
vault-docs.zajaly.dev → Cloudflare Worker → fetches zajaly.gitbook.io/docs → serves content
                                           + Cloudflare Zero Trust login gate
```

**Steps (when ready):**

1. **Create Worker:**
   - Cloudflare Dashboard → **Workers & Pages** → **Create Worker**
   - Write reverse proxy: fetch from `zajaly.gitbook.io/docs`, rewrite links, return content

2. **Set Route:**
   - Worker → **Settings** → **Triggers** → add route: `vault-docs.zajaly.dev/*`

3. **DNS Record:**
   - In Cloudflare DNS: add `A` record for `vault-docs`:
     - IP: `192.0.2.1` (dummy IP — Worker intercepts all traffic)
     - Proxy: **ON** (orange cloud ✅ — required for Worker routing)

4. **Add Zero Trust:**
   - Cloudflare Zero Trust (one.dash.cloudflare.com) → **Access** → **Applications** → **Add**
   - Application type: **Self-hosted**
   - Domain: `vault-docs.zajaly.dev`
   - Policy: allow only your email (or a list of approved emails)
   - Auth method: **One-time PIN** (sends code to approved email)

5. **Result:** `vault-docs.zajaly.dev` prompts for email → sends OTP → shows GitBook content after auth.

**Cost:** $0. Cloudflare Zero Trust free tier = up to 50 users.

> [!CAUTION]
> GitBook's frontend JavaScript may have internal links referencing `*.gitbook.io`. Client-side navigation could break if links aren't rewritten. Test thoroughly. This is an advanced setup — only pursue when you actually need password-protected GitBook docs.

---

## Mintlify — Free Tier Workaround

Mintlify's built-in password protection requires Pro ($250/mo). Same Cloudflare Worker approach works:

1. Set up `private-docs.zajaly.dev` with a Worker proxy pointing to your Mintlify site
2. Add Zero Trust authentication
3. Same cost: $0

**Simpler alternative:** Just use Obsidian Publish for private docs and Mintlify for public docs. Different tools for different audiences.

---

## Cloudflare Zero Trust — Universal Free Authentication

**What it is:** Cloudflare's identity-aware proxy. Free for up to 50 users.

**How it works:** Any request to a protected domain must first authenticate via email OTP (or Google/GitHub SSO). No passwords to manage — users enter their email, receive a one-time code, and get access.

**Compatible with:** Any service behind a Cloudflare-proxied domain.

**Setup overview:**

1. **Cloudflare Zero Trust dashboard:** `one.dash.cloudflare.com`
2. Create an **Access Application** for each protected domain
3. Set policies: which email addresses (or email domains) are allowed
4. Authentication methods:
   - **One-time PIN** (email-based, no external IdP needed) ← simplest
   - Google authentication
   - GitHub authentication
   - Azure AD, Okta (enterprise)

**Free tier limits:** 50 users, unlimited applications. More than enough for a solo dev or small team.

---

## Recommended Protection Strategy

| Content | Where Published | Protection | Method |
|---|---|---|---|
| Private knowledge base | Obsidian Publish (`vault.zajaly.dev`) | ✅ Password | Built-in ($8/mo) |
| Internal SOPs, drafts | Never published (stay in vault) | ✅ Local only | Not on the internet |
| Product docs (Custojo, Waraq) | GitBook (`zajaly.gitbook.io/*`) | Public or Unlisted | GitBook audience setting |
| Dev docs | Mintlify (`docs.zajaly.dev`) | Public | Mintlify free tier |
| Blog | Hashnode (`blog.zajaly.dev`) | Public | Hashnode (always public) |
| Courses | Skillplate (`learn.zajaly.dev`) | Per course | Free/paid/invite-only |
| Changelog | Featurebase (`changelog.zajaly.dev`) | Public | Featurebase |

**Bottom line:** Obsidian Publish at $8/mo is your only affordable password protection. Use it for private content. Everything else is public-facing — protect it with "unlisted" visibility where needed, or Cloudflare Zero Trust if you need real authentication.

---

## Checklist

- [ ] Obsidian Publish password set for `vault.zajaly.dev`
- [ ] GitBook ZajalyDocs space set to **Unlisted** (share link only)
- [ ] GitBook Custojo + Waraq spaces set to **Public**
- [ ] Understand: Mintlify, Hashnode, Featurebase are public on free tiers
- [ ] Skillplate courses configured with correct access level (free/paid/invite)
- [ ] (Optional, future) Cloudflare Zero Trust evaluated for advanced needs

---

*Related: [[02-Obsidian-Setup]] | [[03-GitBook-Free-Setup]] | [[04-Mintlify-Free-Setup]]*
*Save to: C:\Zajaly\ZajalyDocs\_Admin\Setup\08-Password-Protection.md*
*Version: 1.0 — February 19, 2026*
