# Branch protection checklist — EML web projects

Use this checklist when creating a new web repo from the EML template or when auditing an existing repo. The goal: **no code reaches `main` without a reviewed PR that passes automated checks.**

Applies to **Phase 1 (web)** projects only. Unity and Unreal use different review gates — see [PLAN.md](../PLAN.md).

---

## Prerequisites

Complete these before enabling branch protection:

- [ ] Repository lives in the EML GitHub org
- [ ] Default branch is `main`
- [ ] At least one successful CI run exists on `main` (so required checks appear in GitHub settings)
- [ ] `.github/workflows/ci.yml` runs `lint`, `test`, and `build` without `continue-on-error` (remove placeholders once the project is configured)
- [ ] PR template is present (`.github/pull_request_template.md`)
- [ ] `.cursor/skills/eml-code-review/` and `.cursor/REVIEW.md` are in the repo (included in EML template) — see [§4 EML code review](#4-eml-code-review-setup)

---

## 1. Protect `main` (repository settings)

**GitHub → Repository → Settings → Branches → Branch protection rules → Add rule**

| Setting | Value |
|---------|-------|
| **Branch name pattern** | `main` |
| **Require a pull request before merging** | Enabled |
| **Required approvals** | `1` (lead or returning student) |
| **Dismiss stale pull request approvals when new commits are pushed** | Enabled |
| **Require review from Code Owners** | Enabled if `CODEOWNERS` exists (recommended) |
| **Require status checks to pass before merging** | Enabled |
| **Require branches to be up to date before merging** | Enabled |
| **Do not allow bypassing the above settings** | Enabled (admins included, unless lab policy says otherwise) |
| **Restrict who can push to matching branches** | Optional — leave empty to allow PR merges only |
| **Allow force pushes** | Disabled |
| **Allow deletions** | Disabled |

### Required status checks

Add every check that must pass before merge. Typical EML web project:

| Check name (as shown in GitHub) | Source |
|---------------------------------|--------|
| `build` (or your CI job name) | GitHub Actions — `.github/workflows/ci.yml` |

> **Note:** Status check names must match exactly. Open a test PR and wait for checks to run before configuring required checks — GitHub only lists checks that have run at least once.

EML does **not** require Cursor Bugbot. AI code review runs locally via `/review-eml` before the PR opens; the PR template asks authors to confirm they ran it.

---

## 2. Org-wide rulesets (recommended for multiple web repos)

If the EML org has GitHub Team or Enterprise, use **Organization → Settings → Repository → Rules → Rulesets** to apply the same protection to all web repos without configuring each one manually.

Suggested ruleset:

| Field | Value |
|-------|-------|
| **Name** | `EML web — main protection` |
| **Target repositories** | Repos tagged `web` or a named list of Phase 1 repos |
| **Branch target** | Default branch (`main`) |
| **Rules** | Same as [§1](#1-protect-main-repository-settings) |

Rulesets override per-repo branch protection when both exist — document which is authoritative for your org.

---

## 3. CODEOWNERS (optional but recommended)

Create `.github/CODEOWNERS` in each web repo to auto-request reviewers:

```
# Default reviewers for all changes
* @UBC-Emerging-Media-Lab/project-lead-github-handle

# Optional: route by area
# /src/components/ @UBC-Emerging-Media-Lab/frontend-lead
# /docs/ @UBC-Emerging-Media-Lab/project-lead-github-handle
```

Enable **Require review from Code Owners** in branch protection if you use this file.

---

## 4. EML code review setup

EML uses the **`eml-code-review` Cursor skill** instead of Cursor Bugbot. Reviews run locally before opening a PR — no separate Bugbot billing.

### Per-repo files (included in template)

| File | Purpose |
|------|---------|
| `.cursor/skills/eml-code-review/SKILL.md` | Review workflow; invoke with `/review-eml` |
| `.cursor/REVIEW.md` | Project-specific review rules |
| `.github/pull_request_template.md` | Author confirms review was run |

### Per-repo verification

- [ ] `.cursor/REVIEW.md` exists and project-specific rules are filled in
- [ ] `/review-eml` runs successfully in Cursor on a test branch
- [ ] Students know to run `/review-eml` and paste the summary into the PR before opening
- [ ] Reviewers know to check the **EML code review** section in PR descriptions

### Student workflow

1. Finish feature on `feat/*` branch
2. Run `/review-eml` in Cursor
3. Fix Critical and High findings
4. Open PR; paste review summary (or "EML review found no issues") under **EML code review**
5. Wait for CI + human approval

### Reviewer workflow

- Confirm PR includes EML review output
- Re-run `/review-eml` locally on complex PRs if needed
- See [reviewer-guide.md](./reviewer-guide.md)

---

## 5. Additional GitHub settings

| Setting | Location | Recommendation |
|---------|----------|----------------|
| **Secret scanning** | Settings → Code security | Enable (org default if available) |
| **Dependabot alerts** | Settings → Code security | Enable for web repos |
| **Merge button** | Settings → General | Allow **Squash merge** only (keeps history clean for student teams) |
| **Auto-delete head branches** | Settings → General | Enable — matches EML branching policy |
| **Template repository** | Settings → General | Enable on `eml-project-template` only |

---

## 6. What branch protection does *not* cover

| Gap | Mitigation |
|-----|------------|
| Direct pushes to `feat/*` branches | Expected — students need to push feature branches. The gate is at merge to `main`. |
| Unreviewed code sitting on a branch | Policy + Trello hygiene; branches should have open PRs when work is "In Review". |
| Skipping `/review-eml` before PR | PR template checkbox; reviewer checks for review summary; lead spot-audits |
| Human review quality | Use [reviewer-guide.md](./reviewer-guide.md); train leads on AI-assisted PR scrutiny. |
| False positives in AI review | Tune `.cursor/REVIEW.md` each semester; reviewer uses judgment |

---

## 7. Verification checklist (run once per repo)

After configuration, open a **docs-only test PR** (onboarding task):

- [ ] PR is required to merge to `main` — direct push to `main` is rejected
- [ ] CI check runs and is required
- [ ] Merge is blocked without an approving review
- [ ] Merge is blocked when a required check fails
- [ ] PR template renders (What / Why / How tested / EML code review / AI disclosure / Docs)
- [ ] Author ran `/review-eml` and pasted summary (onboarding PR may note "N/A — docs only")
- [ ] Branch is auto-deleted after merge (if enabled)

Record the date and verifier name in `docs/handoff.md` under **Infrastructure** or **Known configuration**.

---

## 8. Post-generation checklist (quick reference)

When creating a repo from the EML template:

- [ ] Complete [github-template-setup.md](./github-template-setup.md) post-generation steps
- [ ] Complete this branch protection checklist
- [ ] Share [reviewer-guide.md](./reviewer-guide.md) with project leads and returning students
- [ ] First student onboarding PR: docs-only change proving the full workflow

---

## Related docs

- [PLAN.md](../PLAN.md) — §3 Source control, §5 Code quality & review
- [github-template-setup.md](./github-template-setup.md) — template repo publishing
- [reviewer-guide.md](./reviewer-guide.md) — what humans check after CI and `/review-eml`
- [REVIEW.md](../template/.cursor/REVIEW.md) — review rules (lives in each project repo)
