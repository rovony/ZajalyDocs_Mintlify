# Zajaly Developer Docs

Public developer documentation for Zajaly APIs, SDKs, and tools. Built with [Mintlify](https://mintlify.com).

**Live site:** [docs.zajaly.dev](https://docs.zajaly.dev)

## Local development

Prerequisites: Node.js v20.17.0+ (LTS recommended), Git.

```bash
git clone git@github.com:rovony/ZajalyDocs_Mintlify.git
cd ZajalyDocs_Mintlify
npm i -g mint
mint dev
```

Preview at [http://localhost:3000](http://localhost:3000). Changes auto-reload on save.

## Deployment

Push to `main` — Mintlify auto-deploys via the GitHub App. No build commands needed.

## Useful commands

| Command | Purpose |
|---|---|
| `mint dev` | Local preview at localhost:3000 |
| `mint dev --port 3333` | Custom port |
| `mint update` | Update CLI to latest version |
| `mint broken-links` | Find broken internal links |
| `mint a11y` | Check accessibility |
| `mint validate` | Validate build (strict mode) |

## Project structure

```
├── docs.json              ← Site config (navigation, theme, settings)
├── index.mdx              ← Home page
├── quickstart.mdx         ← Getting started guide
├── development.mdx        ← Local development instructions
├── essentials/            ← Writing and customization guides
├── api-reference/         ← API documentation + OpenAPI spec
├── ai-tools/              ← AI coding tool setup guides
├── snippets/              ← Reusable content snippets
├── images/                ← Static assets
├── logo/                  ← Brand logos (light + dark)
└── favicon.svg
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.
