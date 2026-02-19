---
name: zajalydocs-process-sources
description: Transforms raw sources from _Inbox, _Sources, or user input into structured ZajalyDocs (guides, series, research notes). Use when processing inbox items, turning external sources into docs, or when the user provides URLs, pasted text, or unorganized material to document.
---

# ZajalyDocs Process Sources

Takes raw or unorganized input and turns it into structured, vault-ready documentation. Vault root: `ZajDocs/`. Paths below are relative to the workspace root unless noted.

## 1. Intake Paths

**A. _Inbox/**  
- Universal capture. Scan for new or unprocessed files.  
- Decide: single note → one doc; multiple topics → multiple docs or one index + links.  
- After processing, move or delete from Inbox; create content in the vault (`ZajDocs/Guides/`, `ZajDocs/Tools/`, `ZajDocs/Defaults/`, etc.).

**B. _Sources/[topic]/**  
- Topic-organized raw material (PDFs, notes, links, snippets).  
- Use when building a guide or series from existing research.  
- Optionally start with a research plan: create a doc from `ZajDocs/Defaults/Templates/Topic-Research-Template.md`, fill "Sources" and "Proposed Structure", then generate the series.

**C. Direct input**  
- User provides: URLs, pasted text, or “turn this into a guide”.  
- Fetch or use the content; analyze scope; then follow the same analysis and output steps below.

## 2. Source Analysis Workflow

1. **Read and summarize**  
   - What is the main topic? Who is it for? What is the outcome (e.g. “get X working”, “decide between A and B”)?

2. **Identify scope**  
   - Single procedure → one guide or SOP.  
   - Broad topic with distinct parts → series (index + numbered files).  
   - Tool evaluation → review or comparison.  
   - Planning / research only → reference using Topic-Research-Template.

3. **Detect gaps**  
   - Missing steps, outdated versions, unclear prerequisites, conflicting info.  
   - List gaps; fill from the web when needed (version numbers, current commands, best practices).  
   - If sources contradict, note in the doc and state the recommended approach with a short reason.

4. **Proposed structure**  
   - For one file: pick template (Guide, SOP, Review, etc.) and folder.  
   - For a series: write a short outline (e.g. 00-Overview, 01-Getting-Started, 02-Config, 99-Troubleshooting) and which template each file uses.

## 3. Decomposition Decision

- **Single file:** One clear task, one audience, &lt; ~10 major steps or sections.  
- **Series:** Multiple audiences, or 5+ major sections, or clear “overview → setup → usage → troubleshooting” split.  
- **Research only:** User wants a plan or outline first → use Topic-Research-Template; “Proposed Structure” and “AI Instructions” drive later generation.

When in doubt, start with one overview file and one “Getting started” file; expand if content grows.

## 4. Series File Naming and Structure

- **Index:** `00-Overview.md` or `README.md` in the topic folder.  
- **Numbered:** `01-Getting-Started.md`, `02-Configuration.md`, … `99-Troubleshooting.md`.  
- Same folder; consistent frontmatter (same `project`, topic `tags`); each file has a clear purpose.  
- Index file links to all others with `[[wikilinks]]`; child files link back to index and to siblings where relevant.

Use the same template type for the whole series when possible (e.g. all guides); mix only when one file is clearly a different type (e.g. one SOP in a guide series).

## 5. Gap-Filling

- **When:** Missing steps, wrong/old commands, unclear prerequisites, or no troubleshooting.  
- **How:** Search the web for current docs, version-specific instructions, and common errors.  
- **In the doc:** Add a short “Sources” or “References” section if you pull a lot from one place; otherwise inline is fine.  
- **Conflicts:** If two sources disagree, pick one as recommended and add a line like “Alternative: [X] suggests Y; we use Z because ….”

## 6. Topic Research Template (Planning Step)

When the user wants a research plan or the topic is large:

1. Create a doc from `ZajDocs/Defaults/Templates/Topic-Research-Template.md`.  
2. Fill **Goal**, **Sources** (title, URL, key points, gaps), **Identified Gaps**, **Proposed Structure** (file list).  
3. In **AI Instructions**, specify: read `_Sources/[topic]/`, fill gaps via search, create the proposed file series, use Guide-Template (or other) per file, cross-link, flag conflicts.  
4. Place in `ZajDocs/Defaults/` or the right topic folder.  
5. Later, use that doc’s “Proposed Structure” and “AI Instructions” to generate the actual series.

## 7. Source Attribution

- For a single primary source: add “Based on [Title](URL)” or “Sources” with links.  
- For many sources: “References” or “Further reading” with a short list.  
- Do not copy large verbatim blocks; summarize and adapt to ZajalyDocs style (second person, steps, expected results).

## 8. Quality Validation Checklist

Before considering processing complete:

- [ ] All required frontmatter on every new file (title, type, status, owner, tags, project, version, created, updated, publish).  
- [ ] Files in correct folders (ZajDocs/Guides/..., ZajDocs/Tools/..., ZajDocs/Defaults/..., or ZajContent/...).  
- [ ] Steps have expected results; code blocks have language tags.  
- [ ] Cross-links between index and child files (and between siblings where useful).  
- [ ] Gaps filled or explicitly called out; conflicts resolved with a stated recommendation.  
- [ ] No raw placeholder text (e.g. `{{title}}` replaced); dates in YYYY-MM-DD.

## 9. After Processing

- Remove or move processed items from `_Inbox/` so they are not reprocessed.  
- Leave `_Sources/` as-is unless the user wants to reorganize; the vault is the source of truth for published structure.
