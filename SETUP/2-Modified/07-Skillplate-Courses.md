---
title: Skillplate + Courses + Video Generation — Complete Guide
type: guide
status: published
owner: Malek
tags: [setup, skillplate, courses, synthesia, video, ai]
project: general
version: 1.0
created: 2026-02-19
updated: 2026-02-19
publish: false
---

# Skillplate + Courses + Video Generation — Complete Guide

> Lifetime deal. AI course builder. Custom domain. Stripe/PayPal payments. Multi-language courses with AI video avatars.

---

## Part A — Skillplate Setup

### What You Have

**Tier 4 Growth Plan** — AppSumo lifetime deal ($349 one-time). No recurring fees ever.

| Feature | Included |
|---|---|
| AI course builder | ✅ |
| Website builder + landing pages | ✅ |
| CRM + email marketing | ✅ |
| Stripe + PayPal payments | ✅ (0% commission) |
| Video lessons, text lessons, file downloads | ✅ |
| Quizzes + certifications | ✅ |
| Analytics + progress tracking | ✅ |
| 180+ app integrations (Zapier, Mailchimp, Zoom, etc.) | ✅ |
| Custom domain | ✅ |
| Multi-language support (EN, ES, AR) | ✅ |
| Community features (Discord integration) | ✅ |
| Membership + subscription management | ✅ |
| Bundles + upsells + cross-sells | ✅ |
| Pre-sales | ✅ |
| Global Brand Kit (logo, colors, fonts) | ✅ |
| Resource library | ✅ |
| Live sessions + coaching (calendar integration) | ✅ |

---

### Step 1 — Activate Account

1. Go to **https://skillplate.com**
2. Log in with your **AppSumo credentials** (or redeem your license code)
3. Create your first academy/workspace → name: `Zajaly Academy` (or `Custojo Academy`)
4. Complete the onboarding wizard

### Step 2 — Configure Branding (Global Brand Kit)

1. Dashboard → **Settings** → **Brand Kit**
2. Upload logo (PNG/SVG — light and dark versions)
3. Set primary brand color (hex code matching your other sites)
4. Set fonts (heading + body)
5. These apply automatically across all pages, checkouts, and course portals

### Step 3 — Connect Payment Gateway

1. Dashboard → **Settings** → **Payments**
2. Connect **Stripe** → follow OAuth flow → select your Stripe account
3. Optionally connect **PayPal** as alternate payment method
4. Set currency (USD, or multi-currency via Stripe)
5. Commission: **0%** — Skillplate takes nothing. Only Stripe's standard processing fee applies.

### Step 4 — Custom Domain (`learn.zajaly.dev`)

1. Dashboard → **Settings** → **Custom Domain**
2. Enter: `learn.zajaly.dev`
3. Skillplate shows the CNAME target
4. In Cloudflare DNS for `zajaly.dev`:

| Type | Name | Target | Proxy |
|---|---|---|---|
| CNAME | `learn` | (as shown in Skillplate settings) | **DNS only** (gray cloud) |

5. Wait for verification (usually 15-60 min)
6. Your course platform is now at `learn.zajaly.dev`

### Step 5 — Create Your First Course

#### Option A — AI Course Builder (fastest)

1. Dashboard → **Courses** → **+ Create Course**
2. Choose **AI Course Builder**
3. Enter topic: e.g., `VPS Server Setup for Laravel Developers`
4. AI generates: complete course outline, module structure, lesson titles, quiz suggestions
5. Review and edit the generated structure
6. Add your content to each lesson (text, video, files)

#### Option B — Manual Builder

1. Dashboard → **Courses** → **+ Create Course**
2. Name: `Server Setup 101`
3. Add modules manually:
   - Module 1: VPS Basics
   - Module 2: SSH Setup
   - Module 3: Security Hardening
4. Add lessons to each module
5. Add content per lesson: text editor, video upload, file attachments, external links

### Step 6 — Lesson Types

| Type | How | Best for |
|---|---|---|
| **Text lesson** | Rich text editor (built-in) | Written tutorials, code walkthroughs |
| **Video lesson** | Upload MP4 or embed YouTube/Vimeo | Visual demos, AI avatar presentations |
| **File download** | Upload PDF, ZIP, any file | Cheatsheets, templates, starter code |
| **External link** | Link to external resource | GitHub repos, documentation sites |
| **Quiz** | AI-generated or manual | Knowledge checks between modules |

### Step 7 — Monetization Options

| Method | How |
|---|---|
| **Free course** | Set price to $0 — used for lead generation |
| **One-time purchase** | Set fixed price (e.g., $49) |
| **Subscription** | Monthly/yearly recurring access |
| **Payment plan** | Split payment over installments |
| **Bundle** | Combine multiple courses at a discount |
| **Pre-sale** | Sell before content is complete |
| **Coupon** | Create discount codes |

### Step 8 — Landing Pages

Skillplate auto-generates a sales page for each course. Customize it:

1. Course → **Landing Page** → edit sections
2. Drag-and-drop builder: hero, features, testimonials, pricing, FAQ
3. AI can generate sales copy for headlines, descriptions, and CTAs
4. Preview on desktop and mobile

### Step 9 — Email Marketing (Built-in)

1. Dashboard → **Email** → create sequences
2. Trigger-based automations:
   - User signs up → Welcome email
   - User completes module → Congratulations + next steps
   - User inactive 7 days → Re-engagement email
   - User purchases → Receipt + onboarding sequence
3. Templates available for common sequences

### Step 10 — Analytics

Dashboard → **Analytics** shows:
- Student enrollment numbers
- Course completion rates
- Revenue per course
- Student progress tracking
- Engagement metrics (lesson views, time spent)

---

## Part B — Course Content Workflow

### Where Course Drafts Live

Course scripts and lesson drafts live in your Obsidian vault:

```
ZajContent/
└── Courses/
    ├── EN/
    │   ├── Server-Setup-101/
    │   │   ├── 00-Course-Overview.md        ← Course description, target audience
    │   │   ├── 01-VPS-Basics.md             ← Lesson script + notes
    │   │   ├── 02-SSH-Setup.md
    │   │   ├── 03-Security-Hardening.md
    │   │   └── Quiz-Questions.md            ← All quiz questions for this course
    │   └── Laravel-Fundamentals/
    │       ├── 00-Course-Overview.md
    │       └── ...
    ├── ES/                                  ← Spanish translations
    │   └── Server-Setup-101/
    │       └── ...
    └── AR/                                  ← Arabic translations
        └── Server-Setup-101/
            └── ...
```

### Content Pipeline

```
1. Research topic → capture in _Inbox/
2. Write detailed guide → ZajDocs/Guides/[topic]/
3. Derive course lessons from guide → ZajContent/Courses/EN/[course]/
4. Add lesson content to Skillplate
5. Generate quiz questions (AI or manual)
6. Create video for lesson (see Part C below)
7. Upload video to Skillplate lesson
8. Set pricing → create landing page → publish
```

### Course Lesson Template

Use this in `ZajDocs/Defaults/Templates/Course-Lesson-Template.md`:

```markdown
---
title: [Lesson Title]
type: course
status: draft
owner: Malek
tags: [course-name, topic]
project: general
version: 1.0
created: {{date}}
updated: {{date}}
publish: false
---

# {{title}}

## Learning Objectives
- [ ] Objective 1
- [ ] Objective 2

## Prerequisites
- What students need before this lesson

## Lesson Content

[Main lesson text here]

## Video Script

[Script for AI video generation — conversational tone, 3-5 min target]

## Quiz Questions

1. Question?
   - A) ...
   - B) ... ← correct
   - C) ...

## Key Takeaways
- Point 1
- Point 2

## Next Lesson
→ [[Next-Lesson-Title]]
```

---

## Part C — AI Video Generation

For course lessons where you want a talking-head video without recording yourself.

### Recommended: Synthesia

**What it does:** Type a script → choose an AI avatar → get a 1080p video of the avatar speaking your content. 230+ avatars, 140+ languages.

**Current pricing (2026):**

| Plan | Price (annual) | Price (monthly) | Video Minutes | Avatars |
|---|---|---|---|---|
| **Free** | $0 | $0 | 3 free videos (watermarked) | Limited |
| **Starter** | $18/mo | $29/mo | 120 min/year (10/mo) | 125+ |
| **Creator** | $64/mo | $89/mo | 360 min/year (30/mo) | 180+ |
| **Enterprise** | Custom | Custom | Unlimited | All 230+ |

**Recommendation:** Start with **Free** to test. Move to **Starter** ($18/mo annual) when you're ready to publish — 120 minutes/year is enough for 20-40 course videos at 3-5 min each.

### Synthesia Workflow

1. Write lesson script in the Course-Lesson-Template's "Video Script" section
2. Go to **synthesia.io** → **Create video**
3. Choose a template (corporate, training, presentation) or start blank
4. Select AI avatar from library
5. Paste script into the voiceover panel
6. Select language and voice
7. Add slides/visuals alongside the avatar if needed
8. Click **Generate** → video renders in minutes
9. Download MP4 (1080p)
10. Upload to Skillplate lesson

### Multi-Language Videos

Synthesia supports 140+ languages. Workflow for localized courses:

1. Write script in English
2. Generate English video → download
3. In Synthesia: **Translate** → select target language (Spanish, Arabic)
4. AI translates script AND generates new video with correct lip-sync
5. Download localized videos
6. Upload each to the matching Skillplate course (EN, ES, AR folders)

### Alternative: HeyGen

Similar to Synthesia, slightly different pricing:
- $24/mo for 15 min of video
- Good lip-sync and avatar realism
- Supports multi-language dubbing
- Worth comparing if Synthesia doesn't fit

### Budget Alternative: Slides + AI Voice (Free)

If Synthesia is too expensive to start:

1. Create slides in **Canva** (free) or PowerPoint
2. Use **ElevenLabs** (elevenlabs.io) free tier for AI voiceover (10 min/mo free)
3. Use **Veed.io** free tier to combine slides + voiceover
4. Result: slide-based video with AI narration, no avatar
5. Upload to Skillplate

**Quality trade-off:** No talking avatar, but functional and free. Good for early courses before investing in Synthesia.

---

## Part D — Skillplate Integration Notes

### Local Folder in _Admin

```
_Admin/Apps/Skillplate/
├── README.md              # How the Skillplate integration works
├── Course-Ideas.md        # Course pipeline and ideas backlog
├── AI-Course-Builder.md   # Tips for using Skillplate's AI effectively
├── Video-Workflow.md      # Video generation steps and settings
└── Email-Sequences.md     # Email automation templates and triggers
```

### Per-Product Course Domains

| Product | Course Domain | Content Focus |
|---|---|---|
| General / Zajaly | `learn.zajaly.dev` | Server setup, Laravel, DevOps, general dev |
| Custojo | `learn.custojo.com` | CRM usage, setup guides, admin training |
| Waraq | `learn.waraq.dev` | IDE usage, developer workflow, extensions |

Each can be a separate Skillplate workspace with its own custom domain, or sections within one workspace.

---

## Checklist

- [ ] Skillplate account activated with AppSumo license
- [ ] Brand Kit configured (logo, colors, fonts)
- [ ] Stripe connected (and/or PayPal)
- [ ] Custom domain `learn.zajaly.dev` configured and verified
- [ ] CNAME record added in Cloudflare (DNS only, gray cloud)
- [ ] First course created (AI builder or manual)
- [ ] At least one video lesson uploaded (Synthesia free test or slides+voiceover)
- [ ] Landing page customized for first course
- [ ] Email automation set up (welcome sequence)
- [ ] Course folder structure created in `ZajContent/Courses/EN/`
- [ ] Course Lesson Template in `ZajDocs/Defaults/Templates/`

---

*Related: [[05-Publishing-Stack]] | [[04-Mintlify-Free-Setup]]*
*Save to: C:\Zajaly\ZajalyDocs\_Admin\Setup\07-Skillplate-Courses.md*
*Version: 1.0 — February 19, 2026*
