# Setup & environment — CODENAME

## Tool versions

| Tool | Version | Notes |
|------|---------|-------|
| Node.js | ≥20 LTS | |
| npm | _bundled_ | |
| Python | ≥3.11 | Required for codetree MCP via `uv` |
| uv | latest | `pip install uv` |
| Cursor | latest | Lab IDE |

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

## Cursor MCP (codetree)

Project config lives in `.cursor/mcp.json`. Prerequisites:

1. Python 3.11+
2. `uv` on PATH
3. Reload Cursor window after clone

Verify: **Cursor → Settings → MCP → codetree** shows connected.

Troubleshooting:

| Symptom | Fix |
|---------|-----|
| MCP red / failed | Install uv; run `uvx --from mcp-server-codetree codetree --help` in terminal |
| Slow first start | codetree builds index on first use; `.codetree/` is gitignored |
| Wrong root | Open repo folder as workspace root, not a parent directory |

## Trello & Harvest

- **Trello board:** _URL_
- **Harvest project:** _URL_ (codename must match board)
- Enable [Harvest ↔ Trello integration](https://www.getharvest.com/apps/trello)

## UBC / lab-specific

- VPN required for: _TBD_
- Shared drives: _TBD_
- Hardware checkout: _TBD_
