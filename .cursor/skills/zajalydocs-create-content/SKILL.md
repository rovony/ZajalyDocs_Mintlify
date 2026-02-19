---
name: zajalydocs-create-content
description: Creates new ZajalyDocs content (guides, SOPs, reviews, comparisons, blog, courses) with correct type, template, folder, and frontmatter. Use when creating new documentation in the ZajalyDocs vault or when the user asks to write a guide, SOP, review, comparison, blog post, or course lesson.
---

# ZajalyDocs Create Content

Creates new documentation in the ZajalyDocs vault following type, template, folder, and frontmatter conventions. Vault root: `ZajDocs/`. All paths below are relative to the vault root unless noted.

## 1. Before Creating

- **Search first:** Check for existing docs on the topic (vault and `_Sources/`).
- **One primary folder:** Place the file where you'd look first; use tags for cross-topic.

## 2. Content Type and Template

| User intent / topic | type | Template path |
|---------------------|------|----------------|
| How-to, steps, tutorial | guide | `Defaults/Templates/Guide-Template.md` |
| Repeatable procedure, policy | sop | `Defaults/Templates/SOP-Template.md` |
| Evaluate one tool | review | `Defaults/Templates/Tool-Review-Template.md` |
| Compare 2+ tools | comparison | `Defaults/Templates/Tool-Comparison-Template.md` |
| Hashnode post | blog | `Defaults/Templates/Blog-Post-Template.md` |
| Skillplate lesson (EN/ES/AR) | course | `Defaults/Templates/Course-Lesson-Template.md` |
| Research plan, topic outline | reference | `Defaults/Templates/Topic-Research-Template.md` |
| Quick lookup, snippet | cheatsheet / snippet | No template; use frontmatter only |

Use the template as the starting body; fill and adjust sections. Replace `{{title}}` and `{{date}}` with real values (YYYY-MM-DD for dates).

## 3. Folder Placement

Paths are under the vault root.

**Guides (topic-first):**

| Topic | Folder |
|-------|--------|
| Servers (SSH, backups, monitoring, security, setup) | `Guides/Servers/` + subdir (e.g. `Backups/`, `SSH/`) |
| Laravel (setup, packages, testing, deployment) | `Guides/Laravel/` + subdir |
| React (components, hooks, state, setup) | `Guides/React/` + subdir |
| Python (setup, scripts, automation) | `Guides/Python/` + subdir |
| Databases (MySQL, PostgreSQL, Redis) | `Guides/Databases/` + subdir |
| Git, CI/CD, Docker, Deployer | `Guides/Git-DevOps/` + subdir |
| REST, webhooks, integrations | `Guides/APIs/` + subdir |
| AI/ML (agents, models, prompts, tools) | `Guides/AI-ML/` + subdir |
| App security, auth, SSL/DNS | `Guides/Security/` + subdir |
| Other / general | `Guides/General/` |

**SOPs:** Same topic folders as guides, or `Defaults/` if cross-cutting.

**Tool reviews:** `Tools/Reviews/`. **Comparisons:** `Tools/Comparisons/`. **Current stack:** `Tools/My-Stack/`.

**Blog:** `ZajContent/Blog/Drafts/` (drafts) or `ZajContent/Blog/Published/` (final). **Courses:** `ZajContent/Courses/{EN|ES|AR}/[Course-Name]/`.

**Research / reference:** `Defaults/` or topic under `Guides/` as appropriate. **Cheatsheets / snippets:** `Defaults/Cheatsheets/`, `Defaults/Snippets/`.

**Product-specific:** Under project folders (e.g. `ZajProjects/Custojo/`, `ZajProjects/Waraq/`) when the doc is for that product only.

## 4. Multi-File Series

Use when the topic is large or has clear parts (e.g. setup → usage → troubleshooting):

- Create an **index file** (e.g. `00-Overview.md` or `README.md`) that links to the rest.
- Create **numbered files** (e.g. `01-Getting-Started.md`, `02-Configuration.md`, `99-Troubleshooting.md`).
- Same folder; same frontmatter conventions; cross-link with `[[wikilinks]]`.

Decide series when: multiple distinct audiences, 5+ major sections, or separate “quick start” vs “deep dive”.

## 5. Frontmatter

Every new file must have:

```yaml
---
title: [Descriptive Title]
type: guide | sop | reference | cheatsheet | snippet | review | comparison | course | blog | template
status: draft
owner: Malek
tags: [relevant, topic, tags]
project: general | custojo | waraq | lms | resiboard | repomemo | deployvault
version: 1.0
created: YYYY-MM-DD
updated: YYYY-MM-DD
publish: false
---
```

- **project:** `general` unless the doc is for one product (then use that product value).
- **tags:** Lowercase, hyphenated. Include topic tags (`servers`, `laravel`, `react`, `python`, `databases`, `git`, `docker`, `security`, `ai-ml`), type (`guide`, `sop`, `review`, `comparison`), and tool name if applicable (e.g. `SimpleBackups`).
- **tool:** Add when the doc is about a specific tool (reviews, setup guides, comparisons).
- **publish:** Set `true` only when ready for Obsidian Publish; default new content to `false`.

Optional by type: `tool`, `next-review` (SOPs), `language`, `course-name`, `module`, `lesson-number`, `duration-minutes`, `has-video` (courses), `target-platform`, `seo-keywords` (blog).

## 6. Cross-Linking

- Search the vault for related notes (same topic, prerequisite guides, tools mentioned).
- Add a **Related** (or **Related Docs**) section with `[[WikiLink]]` to 2–5 relevant docs.
- In body, link to other docs where it helps (e.g. “See [[Other-Guide]].”).

## 7. Publishing Targets

| Content type | Typical platform |
|--------------|-------------------|
| Guides, SOPs, references, cheatsheets | Obsidian Publish (if `publish: true`) |
| Tool reviews, comparisons, setup guides | Obsidian Publish, GitBook, Mintlify (selectively) |
| Blog | Hashnode (from Blog source folder) |
| Courses | Skillplate (from Courses source folder) |
| Product docs | GitBook / Mintlify per product |

Do not set `publish: true` unless the owner has confirmed; default new content to `publish: false`.

## 8. Checklist Before Finishing

- [ ] Content type and template chosen and applied.
- [ ] File placed in the correct folder (vault-relative path).
- [ ] All required frontmatter fields set; dates and title filled.
- [ ] Tags include topic + type (+ tool if applicable).
- [ ] Related docs section with wikilinks.
- [ ] Code blocks have language tags; steps have expected results where applicable.
