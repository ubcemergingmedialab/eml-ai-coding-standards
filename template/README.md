# CODENAME

One-line description of the project.

**Emerging Media Lab (UBC)** · [eml.ubc.ca](https://eml.ubc.ca)

| | |
|---|---|
| **Lead** | [Name](mailto:email@ubc.ca) |
| **Platform** | Web |
| **Term** | e.g. W1 2026 |

## Project links

| Resource | URL |
|----------|-----|
| Trello | _add board URL_ |
| Harvest | _add project URL_ |
| Standards | [eml-ai-coding-standards](https://github.com/UBC-Emerging-Media-Lab/eml-ai-coding-standards) |

## Prerequisites

- Node.js LTS (≥20) — see `.nvmrc` or pin version here
- [uv](https://docs.astral.sh/uv/) (Python package runner, for codetree MCP)
- [Cursor](https://cursor.com) with MCP enabled

## Quick start

```bash
git clone git@github.com:UBC-Emerging-Media-Lab/CODENAME.git
cd CODENAME
npm install
cp .env.example .env   # fill in values
npm run dev
```

## Repository layout

```
src/           Application source
docs/          Architecture, setup, handoff
.cursor/       Cursor MCP + rules (lab standard — commit this)
.github/       PR and issue templates
```

## Development

| Task | Command |
|------|---------|
| Dev server | `npm run dev` |
| Lint | `npm run lint` |
| Test | `npm test` |
| Build | `npm run build` |

## Cursor + codetree MCP

This repo includes lab-standard Cursor configuration:

1. Install **uv**: `pip install uv` (or lab bootstrap script)
2. Open the repo in **Cursor**
3. Go to **Settings → MCP** — `codetree` should show green
4. Agents will use tree-sitter search before reading whole files (see `.cursor/rules/`)

If MCP fails to start, confirm Python 3.11+ and `uvx` are on your PATH.

## Workflow

1. **Trello** — pick a card in **Ready**; link GitHub issue
2. **Harvest** — start timer from the card
3. **Branch** — `feat/short-description` from `main`
4. **Cursor** — implement; disclose AI use in PR
5. **PR** — fill template; get review; merge

See [EML coding standards PLAN.md](https://github.com/UBC-Emerging-Media-Lab/eml-ai-coding-standards/blob/main/PLAN.md).

## Documentation

- [Architecture](docs/architecture.md)
- [Setup & secrets](docs/setup.md)
- [Handoff notes](docs/handoff.md)

## License

<!-- SPDX identifier or "All rights reserved — UBC Emerging Media Lab" -->
