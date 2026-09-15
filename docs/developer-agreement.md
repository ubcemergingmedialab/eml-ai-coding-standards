# EML Developer Agreement

**UBC Emerging Media Lab**  
*AI-Assisted Development Standards Commitment*

---

## Agreement

I, **________________________** (print name), agree to follow the Emerging Media Lab coding standards and development practices as outlined in the [EML AI-Assisted Development Standards](https://github.com/UBC-Emerging-Media-Lab/eml-ai-coding-standards) repository and summarized below.

**Project:** _______________________  
**Platform:** ☐ Web  ☐ Unity  ☐ Unreal  
**Term:** _______________________  
**Date:** _______________________

---

## Core commitments

### 1. Environment & tooling

I will:

- [ ] Install and configure **Cursor IDE** (or approved equivalent) with required MCP tools
- [ ] Set up **tree-sitter MCP** (codetree) for structured code search before raw file reads
- [ ] Use **Git** for all source control; never commit directly to `main`
- [ ] Complete the onboarding checklist within my first week
- [ ] Maintain access to **Trello** and **Github** accounts
- [ ] Use EML-provided coding assistant for EML work **only**
- [ ] Not share access to EML AI services to anyone outside of EML



### 2. AI-assisted workflow

I understand that:

- AI tools (Cursor agents, Copilot, etc.) **assist** development but **do not replace** my responsibility for code quality and correctness
- I must **read, understand, and verify** all AI-generated code before committing
- I will **never** merge AI output without manual testing and review
- I will use **tree-sitter MCP tools** for code navigation before reading entire files
- I will follow platform-specific AI guidance:
  - **Web:** Full AI assistance allowed
  - **Unity:** AI for C# only; no AI edits to `.unity`, `.prefab`, or Project Settings
  - **Unreal:** AI for whitelisted C++ modules only; Blueprints remain human-authored with manual documentation

I will:

- [ ] Disclose AI assistance in every PR using the AI disclosure checkbox
- [ ] Describe which parts were AI-generated and which I wrote or verified
- [ ] Never paste confidential research data or UBC student records into AI tools
- [ ] Use IDE integrations with Trello and Github for workflow automation where convenient



### 3. Source control & Git hygiene

I will:

- [ ] Follow **conventional commit** message format (e.g., `feat(scope): description`)
- [ ] Create feature branches using the naming convention: `feat/*`, `fix/*`, or `docs/*`
- [ ] **Never push directly to** `main` — all changes via pull request only
- [ ] Ensure **CI passes** (lint, test, build) before requesting review
- [ ] Delete branches after merge
- [ ] Keep commits atomic and focused; avoid mixing unrelated changes
- [ ] Never commit secrets, API keys, or credentials to the repository
- [ ] Use `.env.example` for environment variable templates; keep actual secrets in env vars
- [ ] Follow platform-specific asset practices (Git LFS for Unity/Unreal when required)



### 4. Pull requests & code review

I will:

- [ ] Complete the PR template fully — What, Why, How tested, EML review summary, AI disclosure, Docs updated
- [ ] Link every PR to its GitHub issue and Trello card
- [ ] Respond to review feedback within 2 business days
- [ ] Explain my reasoning when disagreeing with review comments
- [ ] Merge only after **≥1 human approval** from a project lead or returning student
- [ ] Test my changes manually using the steps I document in "How tested"
- [ ] Keep PRs reasonably sized (< 500 lines when possible); split large changes into multiple PRs



### 5. Code quality

I will:

- [ ] Follow the project's linting and formatting standards (ESLint, Prettier, `.editorconfig`)
- [ ] Write **tests** for non-trivial logic (critical paths, edge cases, business logic)
- [ ] Handle null/undefined cases, async errors, and loading states
- [ ] Validate external input at system boundaries
- [ ] Use meaningful variable and function names consistent with project conventions
- [ ] Remove debug code (`console.log`, commented blocks) before committing
- [ ] Avoid over-engineering — prefer simple, maintainable solutions



### 6. Security & compliance

I will:

- [ ] Never commit secrets, tokens, API keys, passwords, or PII to the repository
- [ ] Add auth checks on all mutating or sensitive server endpoints
- [ ] Sanitize user input; never use `dangerouslySetInnerHTML` without sanitization
- [ ] Follow UBC IT policies for handling UBC student data or research data
- [ ] Document new environment variables in both `.env.example` and `docs/setup.md`
- [ ] Track open-source dependency licenses; respect Unity/Unreal Asset Store terms



### 7. Documentation

I will:

- [ ] Update **README.md**, `docs/architecture.md`, and `docs/setup.md` when my changes affect setup, architecture, or usage
- [ ] Keep documentation **accurate** — verify AI-generated docs before merging
- [ ] Update `docs/handoff.md` at the end of my term with:
  - Current state (what works, what's broken)
  - In-progress work (branches, WIP PRs)
  - Next priorities for incoming students
  - Gotchas (environment quirks, hardware IDs, setup issues)
- [ ] Export **Blueprint documentation** when working in Unreal (PNG + description in `docs/blueprints/`)



### 8. Project management (Trello)

I will:

- [ ] Link every dev card to its **GitHub issue** in the custom field before moving to **In Progress**
- [ ] Update active cards weekly with three bullets: Done / Doing / Blocked
- [ ] Apply correct labels: platform tag, `this-term`/`future`, `blocked` when applicable
- [ ] Complete the **Definition of Done** checklist before moving cards to **Done**
- [ ] Move incomplete work to **Handoff notes** at term end — never leave work silently in progress



### 9. Collaboration & handoff

I will:

- [ ] Complete the **end-of-term checklist** before leaving:
  - [ ] `docs/handoff.md` complete
  - [ ] All open PRs merged or closed with notes
  - [ ] `main` branch builds and runs from a clean clone
- [ ] Attend retrospectives and provide honest feedback on what worked and what didn't

---



## Platform-specific commitments (use only if relevant)



### Web projects 

- [ ] Follow TypeScript strict mode
- [ ] Ensure `npm run lint`, `npm test`, and `npm run build` pass before every PR
- [ ] Write tests for critical user paths and business logic
- [ ] AI agents may create files, wire routes, and write tests



### Unity projects 

- [ ] AI edits **C# only** in `Assets/Scripts/` (and documented Editor paths)
- [ ] **Never** ask AI to edit `.unity`, `.prefab`, or Project Settings files
- [ ] Use Edit Mode tests (NUnit) for pure C# gameplay logic
- [ ] Include screenshots in PRs when scene structure changes
- [ ] Use Git LFS for assets (`.psd`, `.fbx`, `.wav`, etc.)



### Unreal projects 

- [ ] AI may assist with **C++ only** in whitelisted modules
- [ ] **Blueprints are human-authored** — export PNG + description to `docs/blueprints/` for any changes
- [ ] No AI-generated changes to `.uasset`, config INI, or plugin manifests without lead approval
- [ ] Use `.clang-format` for C++ code formatting

---



## Acknowledgment

I understand that:

1. **I am accountable** for all code I commit, whether AI-assisted or manually written
2. Failure to follow these standards may result in:
  - PRs rejected or blocked from merge
  - Rework required at my own time cost
  - Removal from the project in cases of repeated violations or security breaches
3. These standards exist to ensure:
  - Code quality and maintainability across semester turnovers
  - Security and compliance with UBC policies
  - Effective use of lab resources (Cursor licenses, project budgets, lead time)
  - Successful project handoffs when I complete my term
4. I can ask questions at any time — leads and returning students are available to help
5. Standards may be updated during my term; I will review changes when notified

---



## Signature

**Student name (print):** _________________________________________

**Student signature:** _________________________________________

**Date:** _________________________________________

**Project lead name:** _________________________________________

**Project lead signature:** _________________________________________

**Date:** _________________________________________

---



## References

- **Full standards repository:** [github.com/UBC-Emerging-Media-Lab/eml-ai-coding-standards](https://github.com/UBC-Emerging-Media-Lab/eml-ai-coding-standards)
- **Implementation plan:** [PLAN.md](https://github.com/UBC-Emerging-Media-Lab/eml-ai-coding-standards/blob/main/PLAN.md)
- **Onboarding slideshow:** [docs/slides.html](https://github.com/UBC-Emerging-Media-Lab/eml-ai-coding-standards/blob/main/docs/slides.html)
- **Project template:** [template/](https://github.com/UBC-Emerging-Media-Lab/eml-ai-coding-standards/tree/main/template)
- **Review checklist:** `.cursor/skills/eml-code-review/checklist.md`
- **Trello board setup:** [templates/trello/board-setup.md](https://github.com/UBC-Emerging-Media-Lab/eml-ai-coding-standards/blob/main/templates/trello/board-setup.md)
- **Reviewer guide:** [templates/reviewer-guide.md](https://github.com/UBC-Emerging-Media-Lab/eml-ai-coding-standards/blob/main/templates/reviewer-guide.md)

---

*Document version: 1.1*  
*Based on EML AI-Assisted Development Standards v0.2*  
*Last updated: September 15, 2026*