# GitHub template repository setup

This folder is a **complete EML project scaffold** you can publish as a GitHub template repository. New projects are created via **Use this template → Create a new repository**.

## What is included

```
template/
├── .kiro/
│   ├── REVIEW.md                # EML review rules (used by /eml-code-review)
│   ├── skills/
│   │   └── eml-code-review/     # /eml-code-review skill
│   ├── settings/
│   │   └── mcp.json             # Optional MCP servers (empty/disabled by default)
│   └── steering/
│       ├── code-search.md       # Search discipline + paths to skip
│       └── project.md           # Stack and workflow conventions
├── .github/
│   ├── pull_request_template.md
│   └── ISSUE_TEMPLATE/          # Bug + feature forms (Trello link field)
├── docs/
│   ├── architecture.md
│   ├── setup.md                 # Env vars, secrets, lab-specific setup
│   └── handoff.md
├── src/                         # Application source (empty starter)
├── .env.example
├── .gitignore
├── CHANGELOG.md
├── package.json                 # Placeholder scripts — replace with your stack
└── README.md
```

## Option A — Dedicated template repo (recommended)

Use one repo in the EML GitHub org (e.g. `eml-project-template`) whose **root** is this scaffold.

### 1. Create the repository

```bash
# From eml-ai-coding-standards repo root
cd template
git init
git add .
git commit -m "Initial EML project template with Kiro config"
git branch -M main
git remote add origin git@github.com:UBC-Emerging-Media-Lab/eml-project-template.git
git push -u origin main
```

Adjust org/repo name to match your GitHub org.

### 2. Enable template repository

On GitHub: **Settings → General → Template repository** → check **Template repository**.

### 3. Create a new project

1. Open `eml-project-template` on GitHub
2. Click **Use this template → Create a new repository**
3. Name the repo with the project **codename**
4. Clone and customize (see checklist below)

## Option B — Keep template inside standards repo

Teams can copy the folder manually:

```bash
cp -r template/ ../my-codename/
cd ../my-codename
git init && git add . && git commit -m "Initial commit from EML template"
```

On Windows (PowerShell):

```powershell
Copy-Item -Recurse template ..\my-codename
cd ..\my-codename
git init; git add .; git commit -m "Initial commit from EML template"
```

Option A is better for **Use this template** on GitHub.

## Post-generation checklist

After creating a repo from the template:

- [ ] Replace `CODENAME` in README, `docs/*`, `.kiro/steering/project.md`, `package.json`
- [ ] Update `.kiro/steering/project.md` with actual stack (Next.js, Vite, etc.)
- [ ] Add Trello and Harvest URLs to README and `docs/setup.md`
- [ ] Create matching Trello board ([board-setup.md](./trello/board-setup.md))
- [ ] Create Harvest project (same codename)
- [ ] Replace placeholder `npm` scripts with real dev/lint/test/build commands
- [ ] Complete [branch protection checklist](./github-branch-protection.md) (CI + human review)
- [ ] Customize `.kiro/REVIEW.md` with project-specific review rules
- [ ] Verify `/eml-code-review` runs in Kiro on a test branch
- [ ] Share [reviewer guide](./reviewer-guide.md) with project leads
- [ ] Confirm the `eml-code-review` skill appears in Kiro (Agent Steering & Skills panel)
- [ ] First PR: docs-only update proving workflow (onboarding task)

## Prerequisites for all students

| Tool | Purpose |
|------|---------|
| [Kiro](https://kiro.dev) | AI-assisted IDE |
| Node.js LTS | Web projects (Phase 1) |

## Updating the template

When lab standards change:

1. Edit files in `eml-ai-coding-standards/template/`
2. Sync to `eml-project-template` repo (merge or cherry-pick)
3. Existing projects opt-in via PR — template updates do not auto-apply

## Related docs

- [PLAN.md](../PLAN.md) — full lab standards
- [Branch protection checklist](./github-branch-protection.md) — required checks and review workflow
- [Reviewer guide](./reviewer-guide.md) — human review after CI and `/eml-code-review`
- [Trello board setup](./trello/board-setup.md)
- [Trello card template](./trello/card-template.md)
