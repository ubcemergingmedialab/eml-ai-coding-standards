# Code review guide — EML web projects (Phase 1)

Guide for project leads and returning students who approve PRs on EML web repositories. Automated checks handle the first pass; **your review is the merge gate.**

---

## The three layers

Every PR passes through three layers before merge. Know what each layer covers so you do not duplicate work or miss gaps.

| Layer | Tool | What it catches | What it misses |
|-------|------|-----------------|------------------|
| **CI** | GitHub Actions (`lint`, `test`, `build`) | Syntax, types, formatting, failing tests, broken builds | Logic bugs, UX, security design, architecture fit |
| **AI review** | `/review-eml` skill (local, before PR) | Likely bugs, security anti-patterns, missing tests/docs, acceptance criteria gaps | Domain correctness, product intent, nuanced lab conventions |
| **Human review** | You | Behavior, maintainability, handoff quality, AI verification | — |

**Rule of thumb:** If CI is green and the author ran `/review-eml`, you are not done. You are starting the human review.

---

## When you get a review request

1. **Read the PR template first** — What, Why, How tested, EML code review, AI disclosure, Docs updated.
2. **Check required gates** — CI green, EML review summary present, no unresolved conversations you care about.
3. **Scan the diff** — Focus on files outside your comfort zone; trust CI for style.
4. **Read the EML review summary** — Confirm Critical/High findings were fixed; spot-check Medium items.
5. **Validate behavior** — Pull the branch locally or use a preview deploy when the change is user-facing.
6. **Approve or request changes** — One clear round of feedback is better than five tiny nitpicks.

Move the Trello card to **In Review** when the PR opens; move to **Done** only after merge and issue close.

---

## What to review (human checklist)

### Correctness & behavior

- [ ] Does the change do what the linked GitHub issue / Trello card describes?
- [ ] Are edge cases handled (empty state, errors, loading, permissions denied)?
- [ ] Did the author actually run the manual steps they listed under **How tested**?

### EML code review

- [ ] PR includes output from `/review-eml` (or states "EML review found no issues")
- [ ] All **Critical** and **High** findings are fixed or explicitly justified
- [ ] If no review summary is present, request changes and ask author to run `/review-eml`

### AI-assisted PRs

When **AI disclosure** is checked:

- [ ] Author noted what the agent generated vs what they wrote or verified
- [ ] No hallucinated imports, APIs, or config keys — spot-check suspicious calls
- [ ] No over-abstraction (generic helpers used once, unnecessary design patterns)
- [ ] Tests exist for non-trivial logic — do not accept "CI is green" as proof of behavior
- [ ] You understand the code well enough to explain it to next semester's student

When **No AI assistance** is checked:

- [ ] Spot-check anyway — unchecked box does not guarantee no AI use; focus on quality regardless

### Security & data

- [ ] No secrets in the diff (including test files and comments)
- [ ] New env vars documented in `docs/setup.md` and `.env.example`
- [ ] Auth checks on new or changed server endpoints / server actions
- [ ] No UBC student data or confidential research data in logs or client storage

### Maintainability & handoff

Ask: **"Could the next student understand and change this without asking me?"**

- [ ] Names and structure match existing project conventions (see `.cursor/rules/project.mdc`)
- [ ] Non-obvious logic has a brief comment or is broken into a well-named function
- [ ] No dead code, commented-out blocks, or debug `console.log` left behind
- [ ] Change size is reasonable — large PRs should be split (see below)

### Documentation

- [ ] README / `docs/architecture.md` / `docs/setup.md` updated when the PR template says they should be
- [ ] `CHANGELOG.md` updated for user-visible changes (if the project uses one)

### Dependencies

- [ ] New npm packages are justified (issue discussion or PR explanation)
- [ ] No duplicate libraries solving the same problem already in the project

---

## What not to spend time on

- Formatting ESLint/Prettier already enforces
- Bike-shedding names when the code is consistent with the surrounding file
- Re-typing EML review findings the author has already fixed — verify the fix instead
- Demanding perfection on docs-only or trivial fix PRs used for onboarding

---

## Giving feedback

### Request changes when

- CI failures are unaddressed
- No `/review-eml` summary and author did not run review
- Critical or High EML review findings left unfixed without explanation
- Behavior does not match the issue or is untested
- Security concern (secrets, auth, injection, data exposure)
- Change is too large to review safely — ask for a split
- AI-generated code you do not understand and the author cannot explain

### Approve when

- All required checks pass
- EML review summary present; Critical/High items resolved
- You verified behavior (locally or via described test steps)
- Docs are updated or correctly marked N/A
- You would be comfortable maintaining this code next semester

### Comment style

Be specific and actionable:

```
❌ "This doesn't look right."
✅ "If `fetchUser` returns 404, `user.name` will throw — handle the null case before rendering."
```

Link to project docs or standards when helpful:

```
See docs/architecture.md — new API routes should use the shared handler in src/lib/api/.
```

---

## PR size guidance

| Size | Lines changed (approx.) | Expectation |
|------|-------------------------|-------------|
| **Small** | < 200 | Normal — approve in one pass |
| **Medium** | 200–500 | Acceptable with clear description |
| **Large** | > 500 | Ask to split unless purely mechanical (rename, format, generated) |

Large AI-assisted PRs are a red flag — agents work best in small, bounded tasks.

---

## `/review-eml` workflow for reviewers

Students run `/review-eml` **before** opening the PR and paste the output into the PR description.

As a reviewer:

1. Read the pasted review summary in the PR
2. **True positive still open** — request changes
3. **False positive** — note in PR comment; suggest updating `.cursor/REVIEW.md` if recurring
4. **Complex PR** — check out branch and run `/review-eml` yourself for a second pass

---

## Local review (for complex PRs)

```bash
git fetch origin
git checkout feat/branch-name
npm install
npm run lint && npm test && npm run build
npm run dev   # manual verification
```

Then run `/review-eml` in Cursor on the checked-out branch.

---

## Review turnaround

| Priority | Target response |
|----------|-----------------|
| Blocking a student mid-sprint | Within 1 business day |
| Docs-only / onboarding PR | Same day when possible |
| End-of-semester rush | Same day — do not let PRs pile up |

If you cannot review within 2 business days, comment on the PR and reassign.

---

## End-of-semester

Before students leave:

- [ ] No PRs left open without a note in `docs/handoff.md`
- [ ] All merged code on `main` was reviewed (check branch protection was not bypassed)
- [ ] Retrospective question: Did `/review-eml` catch real issues? Tune `.cursor/REVIEW.md` for next term.

---

## Related docs

- [PLAN.md](../PLAN.md) — §5.4 Human review norms
- [github-branch-protection.md](./github-branch-protection.md) — merge gates and required checks
- [REVIEW.md](../template/.cursor/REVIEW.md) — review rules (per project repo)
- [eml-code-review skill](../template/.cursor/skills/eml-code-review/SKILL.md) — `/review-eml` workflow
- [Trello board setup](./trello/board-setup.md) — **In Review** list workflow
