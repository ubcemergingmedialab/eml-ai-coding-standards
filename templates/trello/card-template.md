# Trello card description template

Copy the block below into a new card description. Replace bracketed placeholders.

---

## Card title format

```
[WEB|UNITY|UE|OPS] Short description
```

Examples:

- `[WEB] Add WebXR session cleanup on unmount`
- `[UNITY] Implement hand-tracking calibration UI`
- `[UE] Export Blueprint docs for grab interaction`
- `[OPS] Book VR lab for demo rehearsal`

---

## Description template

```markdown
## Summary
One or two sentences: what and why.

## Acceptance criteria
- [ ] …
- [ ] …
- [ ] …

## Links
- GitHub issue: [URL or #123]
- PR: [URL when in review]
- Docs: [path in repo, if applicable]

## Notes
Platform/build targets, hardware, dependencies, or screenshots.

---
Platform: web | unity | unreal
VR: yes | no
AI-assisted: yes | no
```

---

## Checklists to attach

### Definition of Ready (before **Ready** → **In Progress**)

- [ ] Acceptance criteria written
- [ ] Platform label applied (`web`, `unity`, `unreal`, or `non-code`)
- [ ] Owner assigned
- [ ] Tagged `this-term` or `future`
- [ ] GitHub issue created (skip if `non-code`)

### Definition of Done (before **Done**)

- [ ] Deliverable complete
- [ ] GitHub issue closed (if applicable)
- [ ] PR merged (if code)
- [ ] Docs updated if behavior changed
- [ ] Harvest time logged with issue # in notes
- [ ] Tested on target platform / hardware

---

## Label guide

| Situation | Labels |
|-----------|--------|
| Web feature, this semester | `web`, `this-term` |
| Unity VR work | `unity`, `vr`, `this-term` |
| Deferred idea | `future` (any platform) |
| Waiting on vendor/UBC IT | `blocked` |
| Equipment booking, admin | `non-code`, `ops` prefix in title |

---

## Harvest logging

When starting work on this card:

1. Open card → **Harvest** → Start timer (or log manually at session end).
2. Select task: **Development**, **AI-assisted dev**, **Design**, etc. (see PLAN.md §9.2).
3. In **Notes**, include: `GitHub #123` and/or this card URL.
4. Stop timer when pausing for the day or switching tasks.

---

## Weekly status (comment on active card)

Post every Friday (or your lab's rhythm):

```
**Done:** …
**Doing:** …
**Blocked:** …
```
