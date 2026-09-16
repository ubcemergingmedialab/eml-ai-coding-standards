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
- [Kiro](https://kiro.dev)

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
.kiro/         Kiro steering, skills, REVIEW.md (lab standard — commit this)
.github/       PR and issue templates
```

## Development

| Task | Command |
|------|---------|
| Dev server | `npm run dev` |
| Lint | `npm run lint` |
| Test | `npm test` |
| Build | `npm run build` |

## Kiro configuration

This repo includes lab-standard Kiro configuration in `.kiro/`:

- `steering/` — always-on project conventions and code-search discipline
- `skills/eml-code-review/` — the `/eml-code-review` pre-PR review skill
- `REVIEW.md` — project review rules the skill reads
- `settings/mcp.json` — optional MCP servers (disabled by default; Kiro has built-in code search, so none are required)

Open the repo in **Kiro** and the steering and skills load automatically. Run `/eml-code-review` before opening a PR.

## Workflow

1. **Trello** — pick a card in **Ready**; link GitHub issue
2. **Harvest** — start timer from the card
3. **Branch** — `feat/short-description` from `main`
4. **Kiro** — implement; disclose AI use in PR
5. **PR** — run `/eml-code-review`, fill template, get review, merge

See [EML coding standards PLAN.md](https://github.com/UBC-Emerging-Media-Lab/eml-ai-coding-standards/blob/main/PLAN.md).

## Documentation

- [Architecture](docs/architecture.md)
- [Setup & secrets](docs/setup.md)
- [Handoff notes](docs/handoff.md)

## License

<!-- SPDX identifier or "All rights reserved — UBC Emerging Media Lab" -->
