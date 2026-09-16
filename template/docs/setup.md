# Setup & environment — CODENAME

## Tool versions

| Tool | Version | Notes |
|------|---------|-------|
| Node.js | ≥20 LTS | |
| npm | _bundled_ | |
| Kiro | latest | Lab IDE |

## First-time setup

```bash
npm install
cp .env.example .env
```

Fill in `.env` locally. **Never commit `.env`.**

## Environment variables

| Variable | Required | Description |
|----------|----------|-------------|
| _Add keys_ | | Document each key |

Production/staging secrets: **GitHub Secrets** or **1Password** (EML vault) — not Trello, not Slack.

## Kiro configuration

Lab-standard Kiro config lives in `.kiro/`:

- `steering/` — always-on project conventions (`project.md`) and code-search discipline (`code-search.md`)
- `skills/eml-code-review/` — the `/eml-code-review` pre-PR review skill
- `REVIEW.md` — project review rules the skill reads

Open the repo folder as the workspace root in Kiro; steering and skills load automatically. Kiro has built-in structured code search, so no MCP server is required. `settings/mcp.json` holds optional servers (disabled by default) — enable one only if the project needs it.

## Trello & Harvest

- **Trello board:** _URL_
- **Harvest project:** _URL_ (codename must match board)
- Enable [Harvest ↔ Trello integration](https://www.getharvest.com/apps/trello)

## UBC / lab-specific

- VPN required for: _TBD_
- Shared drives: _TBD_
- Hardware checkout: _TBD_
