# EML AI-Assisted Development Standards

Standards, templates, and checklists for **Emerging Media Lab** student projects using AI-assisted IDEs (primarily Cursor).

## Start here

- **[PLAN.md](./PLAN.md)** — Full implementation plan: practice categories, phased rollout (web → Unity → Unreal), source control, documentation, tree-sitter MCP, Trello, and Harvest.
- **[docs/slides.html](./docs/slides.html)** — Onboarding slideshow summarizing the standards (open in a browser).
- **Presentation skill** — `.cursor/skills/eml-presentation/` (themeable; EML default).

## Quick links (once templates exist)

| Resource | Purpose |
|----------|---------|
| `templates/cursor/` | MCP config and Cursor rules |
| `templates/docs/` | README, architecture, handoff templates |
| `templates/github-branch-protection.md` | Branch protection checklist (CI + human review) |
| `templates/reviewer-guide.md` | Human code review guide (web Phase 1) |
| `template/.cursor/REVIEW.md` | EML review rules (per project; used by `/review-eml`) |
| `.cursor/skills/eml-code-review/` | `/review-eml` skill — local AI code review |
| `.cursor/skills/eml-presentation/` | HTML briefing slideshows (EML style, themeable) |
| `templates/trello/` | Board setup and card description templates |
| `template/` | **GitHub project template** — `.cursor/`, MCP, docs, issue/PR templates |
| `templates/github-template-setup.md` | How to publish `template/` as a GitHub template repo |
| `checklists/` | Student onboarding and semester handoff |

## Lab policy summary

1. Use **tree-sitter MCP** (codetree) for code search before raw file reads.
2. Every repo: **protected `main`**, PR reviews, **`/review-eml` before PR**, conventional commits.
3. Every repo: **README**, **architecture doc**, **handoff doc** updated each semester.
4. **Trello** for planning; **GitHub Issues** for code tasks; **Harvest** for time — always linked.
5. **Web** — full AI-assisted workflow. **Unity** — C# only. **Unreal** — C++ assist; Blueprints human-documented.

## New project from template

Use [`template/`](./template/) as a GitHub template repository. See [`templates/github-template-setup.md`](./templates/github-template-setup.md) for publishing and post-generation checklist.

Questions: contact your EML project lead.
# eml-ai-coding-standards
