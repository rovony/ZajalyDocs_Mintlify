# Zajaly Developer Docs — Agent Instructions

## About this project

- Public developer documentation for Zajaly APIs, SDKs, and tools
- Built on [Mintlify](https://mintlify.com) — deployed at `docs.zajaly.dev`
- Pages are MDX files (Markdown + JSX components) with YAML frontmatter
- Configuration lives in `docs.json`
- Auto-deploys on push to `main` via the Mintlify GitHub App

For Mintlify component reference and configuration options, consult [mintlify.com/docs](https://mintlify.com/docs).

## Repository

- **GitHub:** `rovony/ZajalyDocs_Mintlify`
- **Live site:** `docs.zajaly.dev` (default: `zajalydocs-mintlify.mintlify.app`)
- **Config:** `docs.json` (not `mint.json` — that format is deprecated)

## CLI commands

- `mint dev` — local preview at localhost:3000
- `mint broken-links` — check for broken internal links
- `mint a11y` — check accessibility (contrast, missing alt text)
- `mint validate` — strict build validation

## Terminology

- Use **"docs"** not "documentation site" in casual references
- Use **"Zajaly"** not "zajaly" in prose (capitalize)
- Use **"API key"** not "token" for authentication credentials
- Products: **Custojo**, **Waraq**, **LMS**, **ResiBoard**, **RepoMemo**, **DeployVault**

## Style preferences

- Active voice, second person ("you")
- Sentence case for headings ("Getting started", not "Getting Started")
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, and code references
- No marketing language ("powerful", "seamless", "robust")
- No filler phrases ("it's important to note", "in order to")

## Content boundaries

- This repo is for **developer-facing** documentation only
- Internal SOPs, knowledge base, and guides live in `rovony/ZajalyDocs` (GitBook)
- Content flows one-way: ZajalyDocs → ZajalyDocs_Mintlify (manual adaptation)
- Do not publish internal operational content, credentials, or admin procedures
