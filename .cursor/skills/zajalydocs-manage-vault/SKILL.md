---
name: zajalydocs-manage-vault
description: Audits and maintains the ZajalyDocs vault (frontmatter, broken links, status, archive). Use when auditing the vault, finding broken wikilinks, reviewing outdated content, archiving deprecated docs, or performing weekly vault health checks.
---

# ZajalyDocs Manage Vault

Audits, maintains, and improves the documentation vault. Vault root: `ZajDocs/`. Paths are relative to the vault root unless noted.

## 1. Health Check Checklist (Weekly)

Run through these in order:

- [ ] **Frontmatter audit:** All `.md` files have required fields (see below).  
- [ ] **Broken wikilinks:** Find `[[...]]` that point to missing or renamed files; fix or remove.  
- [ ] **Status review:** Any `outdated` or `needs-review` docs updated or status changed.  
- [ ] **Orphaned files:** No important docs in wrong folders; move if needed.  
- [ ] **Empty or stub files:** Either fill or mark `status: draft` and add a one-line purpose.  
- [ ] **Changelog:** SOPs and any doc with a changelog table have new changes logged.

## 2. Frontmatter Audit

**Required fields for every `.md` in the vault:**

- `title`, `type`, `status`, `owner`, `tags`, `project`, `version`, `created`, `updated`, `publish`

**Checks:**

- `type` is one of: guide, sop, reference, cheatsheet, snippet, review, comparison, course, blog, template.  
- `status` is one of: draft, review, published, outdated, archived.  
- `project` is one of: general, custojo, waraq, lms, resiboard, repomemo, deployvault.  
- `tags` is an array; prefer lowercase, hyphenated.  
- `created` and `updated` are YYYY-MM-DD.  
- `publish` is boolean (true/false).

Fix: Add missing fields with sensible defaults (`status: draft`, `publish: false`, `version: 1.0`, today for dates). If a file is clearly published, set `publish: true` and `status: published` only when appropriate.

## 3. Broken Link Detection

1. **Collect wikilinks:** Grep for `\[\[([^\]]+)\]\]` in all `.md` files.  
2. **Resolve target:** Each `[[Target]]` or `[[Target|Label]]` refers to a note; the target is the file name (with or without `.md`).  
3. **Check existence:** For each target, a file should exist (same name or with `.md`). Ignore anchors (e.g. `#heading`) for existence check if your tool doesn’t resolve them.  
4. **Report:** List file → broken link. Fix by: renaming the target file to match, updating the link, or removing the link and adding a note if the doc was archived.

Optional: Use an Obsidian or Markdown plugin that reports broken links; same idea.

## 4. Status Lifecycle

- **draft** → Work in progress; not ready for review.  
- **review** → Ready for human review before publish.  
- **published** → Reviewed and live; keep `updated` current when you change the doc.  
- **outdated** → Known to be out of date; needs update or deprecation.  
- **archived** → No longer active; moved to `_Archive/`, not published.

**Transitions:**

- When content is factually wrong or obsolete: set `status: outdated` (and bump `updated`), or move to archive and set `status: archived`.  
- When a doc is fully replaced by another: add a one-line note at the top pointing to the new doc; then archive the old one.  
- When updating a published doc: change `updated`, and if the change is major, bump `version` and add a changelog entry if the file has a changelog table.

## 5. Archive / Deprecation Workflow

1. **Decide:** Content is superseded, wrong, or no longer relevant.  
2. **Redirect (optional):** In the doc to archive, add at the top: “Superseded by [[New-Doc]].” or “Deprecated. See [[Other]].”  
3. **Move:** Move file to `_Archive/` (optionally keep a subfolder by topic or date).  
4. **Frontmatter:** Set `status: archived`, `publish: false`. Update `updated`.  
5. **Fix incoming links:** Search for `[[FileName]]` (and `[[FileName|...]]`) across the vault; update those links to point to the new doc or remove the link.

Do not delete; archive so history is kept.

## 6. Reorganization Rules

- **One primary folder:** A doc lives in the folder where you’d look first (e.g. by topic under Guides/, or Tools/Reviews/, or ZajProjects/ProductName/).  
- **Cross-topic:** Use tags; don’t duplicate the file in multiple folders.  
- **When moving:** Update any wikilinks that point to the moved file (links are usually by note name, so they may still work; verify). Update `updated` and changelog if present.  
- **Naming:** Use clear, descriptive filenames; avoid special characters. For series, use the numbering scheme (00-Overview, 01-..., 99-Troubleshooting).

## 7. Version Bumping

- **Major content change:** New sections, rewritten procedures, or important corrections → bump `version` (e.g. 1.0 → 1.1 or 2.0).  
- **Minor:** Typo fixes, small clarifications → update `updated` only.  
- **Changelog:** If the file has a Changelog table, add a row: version, date, short description of change.

## 8. Useful Dataview Queries (Vault Maintenance)

Run these in Obsidian (Dataview plugin) or adapt for scripts. Scope to the vault folder.

**Drafts (recent):**
```dataview
TABLE title, type, project, created
FROM ""
WHERE status = "draft"
SORT created DESC
LIMIT 20
```

**Outdated / needs review:**
```dataview
TABLE title, type, updated
FROM ""
WHERE status = "outdated" OR status = "review"
SORT updated ASC
```

**Published docs:**
```dataview
TABLE title, type, project
FROM ""
WHERE publish = true
SORT file.folder ASC
```

**Guides by topic:**
```dataview
TABLE title, status, updated
FROM "Guides"
WHERE type = "guide"
SORT file.folder ASC
```

**No tags (possible frontmatter issue):**
```dataview
LIST title
FROM ""
WHERE length(tags) = 0
```

**Recently updated (last 30 days):**
```dataview
TABLE title, type, updated
FROM ""
WHERE date(updated) >= date(today) - dur(30 days)
SORT updated DESC
```

Use these to find candidates for review, archive, or frontmatter fixes.

## 9. Audit Report Outline

When producing an audit report, include:

1. **Frontmatter:** Count of files missing required fields; list of files to fix.  
2. **Broken links:** File and link text for each broken `[[...]]`.  
3. **Status:** Counts by status; list of `outdated` and `review` with age.  
4. **Suggestions:** Docs to archive, merge, or split; folders to reorganize.  
5. **Optional:** Dataview query results (drafts, outdated, published) as appendices.

Keep the report actionable: clear next steps and file paths.
