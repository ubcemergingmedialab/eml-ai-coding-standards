---
name: eml-code-review
description: >-
  Review code changes against EML web project standards (security, correctness,
  tests, docs, AI-generated code scrutiny). Use when the user asks for
  /eml-code-review, EML code review, pre-PR review, or review before opening a
  pull request.
---

# EML Code Review

Perform a structured code review for EML Phase 1 web projects. Reviews run locally in Kiro using normal agent usage — no separate review service or billing.

## When to use

- User runs `/eml-code-review` or asks for an EML code review
- Before opening a PR (required by EML workflow)
- Reviewer wants a second AI pass on a branch

## Review workflow

1. **Identify the repository root** — use the active workspace or the path the user specifies.

2. **Load standards** (read in this order):
   - `.kiro/REVIEW.md` — project review rules (required in EML web repos)
   - `.kiro/steering/project.md` — stack and conventions
   - [checklist.md](checklist.md) — condensed fallback if `REVIEW.md` is missing

3. **Determine the diff scope**:
   - Default: **branch changes** — diff against merge-base with `main` (or repo default branch), including committed, staged, and unstaged changes
   - If user asks for uncommitted/dirty/working-tree only: **uncommitted changes**
   - If user specifies a base branch: compare against that branch

   Use git to compute the diff. Do not review files in `node_modules/`, `dist/`, `.next/`, `build/`, or lockfiles unless the change is suspicious.

4. **Load issue context** (when available):
   - Parse branch name for issue number (e.g. `feat/42-add-login`)
   - Or ask the user for the GitHub issue number if not obvious
   - Read the issue (GitHub MCP, `gh issue view`, or user-provided text) for acceptance criteria
   - Flag changes that do not map to acceptance criteria or expand scope beyond the issue

5. **Review the diff** against standards. Prioritize:
   1. Security (secrets, auth, injection, data exposure)
   2. Correctness (logic bugs, async, error handling)
   3. Acceptance criteria coverage (if issue linked)
   4. Regression risk (missing tests on non-trivial logic)
   5. Maintainability and handoff quality
   6. Documentation gaps

   Do not nitpick formatting ESLint/Prettier already enforces in CI.

6. **Output findings** — see [Output format](#output-format) below.

7. **Do not fix findings** unless the user explicitly asks. Do not rerun unless asked.

## Output format

If no diff or empty diff: one sentence stating there was nothing to review.

If no issues: one line — `EML review found no issues.`

If issues found, print:

```markdown
## EML code review — [branch name or "uncommitted changes"]

**Scope:** [branch changes | uncommitted changes] vs [base branch]
**Issue:** [#N title](url) or "none linked"

| Severity | Location | Finding |
|----------|----------|---------|
| Critical | `path/to/file.ts:42` | … |
| High | … | … |
```

Sort rows by severity: Critical → High → Medium → Low.

### Severity definitions

| Severity | Meaning |
|----------|---------|
| **Critical** | Must fix before PR — security flaw, data loss, auth bypass, broken core flow |
| **High** | Should fix before PR — likely bug, missing auth check, no tests on important logic |
| **Medium** | Fix or discuss — maintainability, missing docs, weak error handling |
| **Low** | Optional — minor clarity, non-blocking suggestions |

After the table, add a short **Summary** (2–3 sentences) and **Acceptance criteria** section if an issue was linked:

```markdown
### Acceptance criteria
- [x] Criterion met — evidence
- [ ] Criterion not met — what's missing
```

Tell the user to paste the review summary into the PR description under **EML code review** when opening the PR.

## Special cases

### Review a specific branch or PR

If the user provides a PR link, branch name, or PR number:

1. Resolve to the head branch
2. Check out that branch locally if needed (stash only after user confirms if checkout is blocked)
3. Run the review on that branch's changes vs base

### Diff cannot be computed

If git diff fails (empty repo, no commits, etc.):

1. Ask the user which files changed, or
2. Read files they specify and review those directly
3. Note in output that review was file-based, not diff-based

### Reviewer running on someone else's PR

Same workflow. Emphasize acceptance criteria and behavior over style. Note anything the PR author should have caught in `/eml-code-review`.

## What this skill does not do

- Post comments on GitHub PRs (paste output into PR manually)
- Replace CI (`lint`, `test`, `build` still required)
- Replace human approval (required by branch protection)
- Run automatically on PR push (students run locally before opening PR)

## Additional resources

- Full review rules: `.kiro/REVIEW.md`
- Human reviewer guide: [reviewer-guide.md](../../../../templates/reviewer-guide.md) in standards repo
- Lab plan: [PLAN.md](../../../../PLAN.md) §5
