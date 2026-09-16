# EML Code Review Requirements — Human Guide

A friendly guide to code review expectations at the UBC Emerging Media Lab for Phase 1 web projects.

---

## Why We Review Code

Code review at EML serves three purposes:

1. **Catch bugs early** — before they reach production
2. **Maintain quality** — ensure code is maintainable across semesters
3. **Support handoffs** — make sure the next student can understand and build on your work

---

## The Review Process (Quick Overview)

Every code change goes through **three layers of review** before it can be merged:

```
┌─────────────────────────────────────────────────────┐
│ 1. CI Checks (automated)                            │
│    • Linting, tests, build verification             │
└─────────────────────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────┐
│ 2. AI Review (you run /eml-code-review before PR)   │
│    • Security, bugs, missing tests/docs             │
└─────────────────────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────┐
│ 3. Human Review (project lead approves)             │
│    • Behavior, maintainability, handoff readiness   │
└─────────────────────────────────────────────────────┘
```

**Important:** All three layers are required — CI green doesn't mean you're done!

---

## For Students: Before You Open a PR

### Required Steps

1. **Make sure CI is passing** (lint, test, build)
2. **Run `/eml-code-review` in Kiro**
   - This reviews your branch changes against EML standards
   - Fix all **Critical** and **High** findings
   - Explain or fix **Medium** findings
3. **Paste the review output into your PR description**
4. **Fill out the PR template completely**
   - What changed and why
   - How you tested it manually
   - Whether AI assisted you (and what you verified)
   - What docs you updated

### What `/eml-code-review` Checks

The AI review looks for these issues (in priority order):

| Priority | What It Catches |
|----------|----------------|
| **Critical** | Security flaws, data loss, broken core features, auth bypass |
| **High** | Likely bugs, missing auth checks, untested critical logic |
| **Medium** | Maintainability issues, missing docs, weak error handling |
| **Low** | Minor improvements, optional suggestions |

### Common Issues Caught by `/eml-code-review`

✅ **Security**
- Hardcoded secrets or API keys
- Missing authentication on server endpoints
- Unsafe HTML rendering without sanitization
- Secrets in client code or URLs

✅ **Correctness**
- Null/undefined not handled properly
- Async errors not caught
- React hooks with stale closures or missing cleanup
- Hallucinated imports (packages that don't exist)

✅ **Testing**
- Missing tests on new business logic
- Changed behavior without test coverage

✅ **Documentation**
- New environment variables not in `.env.example` or `docs/setup.md`
- Changed architecture without updating `docs/architecture.md`

✅ **AI-Generated Code Issues**
- Over-engineering (unnecessary abstractions)
- Incomplete wiring (new UI without route, route without auth)
- Plausible but incorrect logic
- Copy-paste inconsistencies

---

## For Reviewers: What to Check

### Your Job

CI and AI review catch *syntax and patterns*. **You catch:**
- Does it actually work as intended?
- Will the next student understand this?
- Does it follow our project conventions?
- Did the author test what they claim?

### Review Checklist

#### ✓ Required Gates
- [ ] CI is passing (green checks)
- [ ] EML review summary is present in PR description
- [ ] Critical and High findings are resolved
- [ ] PR template is filled out

#### ✓ Correctness & Behavior
- [ ] Change matches the linked GitHub issue/Trello card
- [ ] Edge cases are handled (empty state, errors, loading, permissions)
- [ ] Author actually tested manually (pull the branch if user-facing)

#### ✓ AI-Assisted PRs (when disclosed)
- [ ] Author noted what was generated vs. verified
- [ ] No hallucinated APIs or imports
- [ ] Tests exist for non-trivial logic
- [ ] No over-abstraction (complex patterns for simple tasks)
- [ ] You understand the code well enough to explain it

#### ✓ Security & Data
- [ ] No secrets in the code (including tests and comments)
- [ ] New env vars are documented properly
- [ ] Auth checks on new/changed server endpoints
- [ ] No student data or research data in logs/localStorage

#### ✓ Maintainability
- [ ] Code follows existing project conventions
- [ ] Non-obvious logic has brief comments
- [ ] No dead code or leftover debug statements
- [ ] PR size is reasonable (< 500 lines unless mechanical)

#### ✓ Documentation
- [ ] README/architecture/setup docs updated when needed
- [ ] CHANGELOG updated for user-visible changes

### When to Request Changes

**You must request changes if:**
- CI is failing
- No `/eml-code-review` summary present
- Critical/High findings are unresolved without explanation
- Behavior doesn't match the issue
- Security concerns exist
- PR is too large to review safely
- AI-generated code you don't understand and author can't explain

**You should approve when:**
- All required checks pass
- EML review summary present and Critical/High items resolved
- You verified the behavior works
- Docs are updated appropriately
- You'd be comfortable maintaining this code next semester

### How to Give Good Feedback

**Be specific and actionable:**

❌ Bad: "This doesn't look right."

✅ Good: "If `fetchUser` returns 404, `user.name` will throw — handle the null case before rendering."

**Link to docs when helpful:**

```
See docs/architecture.md — new API routes should use the 
shared handler in src/lib/api/.
```

---

## What We DON'T Review

**Skip these to focus on what matters:**

- ❌ Formatting that ESLint/Prettier already enforces
- ❌ Style nitpicks when code is consistent with the file
- ❌ Lockfile-only changes (unless dependency is suspicious)
- ❌ Subjective naming preferences
- ❌ Missing tests on trivial one-line fixes (typos, config)

---

## Severity Definitions (Quick Reference)

| Severity | When to Use | Examples |
|----------|-------------|----------|
| **Critical** | Must fix before merge — breaks core functionality or security | Auth bypass, data loss, exposed secrets, broken login |
| **High** | Should fix before merge — likely bugs or risks | Missing auth check, untested critical logic, uncaught promise rejections |
| **Medium** | Fix or discuss — impacts maintainability | Missing docs, unclear naming, weak error messages |
| **Low** | Optional — nice-to-haves | Minor clarity improvements, suggestions |

---

## PR Size Guidelines

| Size | Lines Changed | Expectation |
|------|--------------|-------------|
| **Small** | < 200 | Normal — one-pass approval expected |
| **Medium** | 200-500 | Acceptable with clear description |
| **Large** | > 500 | Should be split unless mechanical (rename, formatting, generated code) |

**Tip:** Large AI-assisted PRs are a red flag. Agents work best in small, focused tasks.

---

## Review Turnaround Expectations

| Priority | Target Response |
|----------|----------------|
| Blocking a student mid-sprint | Within 1 business day |
| Docs-only or onboarding PR | Same day when possible |
| End-of-semester rush | Same day — don't let PRs pile up |

If you can't review within 2 business days, comment on the PR and reassign.

---

## Special Cases

### Reviewing a Specific Branch or PR

If someone asks you to review a specific branch:
1. Check out the branch locally
2. Run `/eml-code-review` yourself
3. Pull the branch and test manually if user-facing
4. Focus on behavior and maintainability

### When `/eml-code-review` Finds False Positives

If the AI review flags something incorrectly:
1. Note it in the PR comment
2. Suggest updating `.kiro/REVIEW.md` if it's recurring
3. Don't require the author to fix non-issues

### Empty or Small Diffs

If git diff is empty or very small (one-line config change):
- Skip intensive review
- Just verify CI is green and change is intentional

---

## Tools & Commands Reference

### For Students (Before PR)

```bash
# Run CI checks locally
npm run lint
npm test
npm run build

# Review your changes in Kiro
/eml-code-review
```

### For Reviewers (Complex PRs)

```bash
# Check out the PR branch
git fetch origin
git checkout feat/branch-name

# Run checks locally
npm install
npm run lint && npm test && npm run build

# Test manually
npm run dev

# Run your own review
/eml-code-review
```

---

## Quick Dos and Don'ts

### ✅ Do

- Run `/eml-code-review` before every PR
- Fix Critical and High findings
- Test your changes manually
- Fill out the PR template completely
- Link your GitHub issue
- Document new environment variables
- Add tests for non-trivial logic
- Ask questions if AI generated code you don't understand

### ❌ Don't

- Skip `/eml-code-review` because "CI is green"
- Commit secrets, API keys, or tokens
- Leave dead code or debug logs
- Submit 1000-line PRs
- Assume AI-generated code is correct without verification
- Ignore review feedback without discussion
- Merge without human approval

---

## Where to Get Help

- **Review not working?** Check `.kiro/REVIEW.md` in your project
- **False positives?** Discuss with your project lead
- **Don't understand a finding?** Ask in your project channel or PR comments
- **Review too strict or too lenient?** Suggest changes to `.kiro/REVIEW.md`

---

## End-of-Semester Checklist

Before students leave for the semester:

- [ ] All open PRs are merged or noted in `docs/handoff.md`
- [ ] All merged code was properly reviewed
- [ ] Retrospective: Did `/eml-code-review` catch real issues?
- [ ] Update `.kiro/REVIEW.md` based on what you learned

---

## Related Documentation

For more detail, see:

- **PLAN.md §5** — Full review workflow and rationale
- **templates/reviewer-guide.md** — Detailed reviewer checklist
- **.kiro/REVIEW.md** — Project-specific review rules (in each project repo)
- **.kiro/skills/eml-code-review/SKILL.md** — How `/eml-code-review` works
- **templates/github-branch-protection.md** — Branch protection setup

---

## Summary: Three Key Principles

1. **Three layers, all required** — CI + AI review + human approval
2. **Security and correctness first** — then maintainability, then style
3. **Handoff-ready code** — the next student should understand it

Code review at EML isn't about perfection — it's about **sustainable quality across semesters**.
