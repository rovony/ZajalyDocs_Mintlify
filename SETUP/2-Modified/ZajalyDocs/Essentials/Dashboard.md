---
title: Dashboard
type: reference
status: published
owner: Malek
tags: [dashboard, index]
project: general
version: 1.0
created: 2026-02-18
updated: 2026-02-18
publish: true
---

# Dashboard

## Recent Drafts
```dataview
TABLE title, type, project, created
FROM ""
WHERE status = "draft"
SORT created DESC
LIMIT 15
```

## Outdated Content (Needs Review)
```dataview
TABLE title, type, updated
FROM ""
WHERE status = "outdated"
SORT updated ASC
```

## All Published Docs
```dataview
TABLE title, type, project
FROM ""
WHERE publish = true
SORT file.folder ASC
```

## Guides by Topic
```dataview
TABLE title, status, updated
FROM "Guides"
WHERE type = "guide"
SORT file.folder ASC
```

## Project Docs
```dataview
TABLE title, type, status
FROM "Projects"
SORT project ASC
```

## Tool Reviews
```dataview
TABLE title, status, updated
FROM "Tools/Reviews"
SORT updated DESC
```

## Recent Blog Drafts
```dataview
TABLE title, status, created
FROM "Blog"
WHERE status = "draft"
SORT created DESC
```
