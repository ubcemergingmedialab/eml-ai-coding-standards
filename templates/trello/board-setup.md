# Trello board setup — EML project template

Use this checklist when spinning up a new project board. The board name is the project **codename** (same name as the Harvest project and referenced in the GitHub repo README).

---

## 1. Create the board

- [ ] Create board named with project codename
- [ ] Set visibility: **Workspace visible** (or lab-standard setting)
- [ ] Add board description:

  ```
  EML project — [codename]
  Lead: [name]
  Repo: [GitHub URL]
  Harvest: [Harvest project link]
  Platform: Web | Unity | Unreal | Mixed
  Term: [e.g. W1 2026]
  ```

- [ ] Invite all team members and project lead
- [ ] Pin board to workspace sidebar

---

## 2. Create lists

Create these lists **in order** (left to right):

| # | List name | Purpose |
|---|-----------|---------|
| 1 | **Backlog** | All ideas; tag with `this-term` or `future` |
| 2 | **Ready** | Scoped work waiting to start |
| 3 | **In Progress** | Active work |
| 4 | **In Review** | PR open or awaiting review |
| 5 | **Done** | Completed this term |
| 6 | **Handoff notes** | Context for incoming cohort |

Optional: Add a **Templates** list (hidden/archived) containing the template card below.

---

## 3. Enable Power-Ups

| Power-Up | Purpose |
|----------|---------|
| **Custom Fields** | GitHub issue URL, owner, grant code, est. hours |
| **GitHub** | Attach PRs and issues to cards |
| **Harvest** | Start/stop timers from cards |

### Custom fields to create

| Field name | Type | Notes |
|------------|------|-------|
| GitHub issue | Text (URL) | Required before **In Progress** for code work |
| Owner | Text | Or use card members |
| Grant / client code | Dropdown | Match Harvest client list |
| Est. hours | Number | Optional |

---

## 4. Create labels

Add these labels on every EML project board:

| Label | Suggested color |
|-------|-----------------|
| `web` | Blue |
| `unity` | Green |
| `unreal` | Purple |
| `vr` | Orange |
| `this-term` | Yellow |
| `future` | Gray |
| `blocked` | Red |
| `non-code` | Black |

---

## 5. Butler automations

Enable **Butler** and create these rules:

### Rule 1 — In Progress reminder

- **When:** Card moved into list **In Progress**
- **If:** Custom field "GitHub issue" is empty **and** card does not have label `non-code`
- **Then:** Add comment: "⚠️ Link a GitHub issue before starting dev work."

### Rule 2 — In Review reminder

- **When:** Card moved into list **In Review**
- **Then:** Add comment: "Link PR in GitHub issue. Confirm CI is green."

### Rule 3 — Blocked notification

- **When:** Label `blocked` added to card
- **Then:** Notify board admins (or post @mention to lead)

### Rule 4 — Done timestamp

- **When:** Card moved into list **Done**
- **Then:** Add comment: "Completed on {date} {time}."

---

## 6. Connect Harvest

- [ ] In Harvest: confirm project exists under correct client (codename matches board)
- [ ] In Harvest: add standard tasks (see [PLAN.md §9.2](../../PLAN.md#92-standard-task-categories))
- [ ] Enable [Harvest ↔ Trello integration](https://www.getharvest.com/apps/trello)
- [ ] Map this Trello board to the Harvest project
- [ ] Verify: open a test card → start Harvest timer → stop → entry appears in Harvest

---

## 7. Connect GitHub

- [ ] Enable **GitHub Power-Up** on the board
- [ ] Connect EML GitHub organization
- [ ] Attach repo to board settings (if supported)
- [ ] Verify: attach a test issue/PR to a card

---

## 8. Seed the board

Create these starter cards:

### Card A — Board template (keep in Templates list or top of Backlog)

- Title: `[TEMPLATE] Feature card — copy me`
- Description: paste from [`card-template.md`](./card-template.md)
- Checklists: copy Definition of Ready and Definition of Done from PLAN.md §8.5

### Card B — Term scope (pin to top of Backlog)

- Title: `[OPS] W_ 20__ term scope`
- Labels: `this-term`, `non-code`
- Description: link to faculty/grant deliverables for this semester

### Card C — Onboarding (Ready list at term start)

- Title: `[OPS] Student onboarding — [name]`
- Labels: `non-code`
- Checklist:
  - [ ] GitHub org access
  - [ ] Kiro set up (steering + skills load)
  - [ ] Harvest access + first time entry
  - [ ] Clone repo; run setup
  - [ ] Docs-only first PR merged
  - [ ] Read PLAN.md + project README

---

## 9. Link from repo

Add to project `README.md`:

```markdown
## Project links

| Resource | URL |
|----------|-----|
| Trello | [board URL] |
| Harvest | [project URL] |
```

---

## 10. Lead sign-off

- [ ] All lists, labels, fields, and Butler rules in place
- [ ] Harvest and GitHub integrations verified
- [ ] Team walked through workflow (Trello → GitHub → Harvest → Kiro)
- [ ] `this-term` scope agreed and tagged on backlog cards
