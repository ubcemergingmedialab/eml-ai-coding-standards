# Code review rules — CODENAME

Replace `CODENAME` with this project's codename. The `eml-code-review` skill (invoke with `/eml-code-review`) reads this file when reviewing branch changes before a PR.

**Stack:** Web (Phase 1) — TypeScript strict, Node.js LTS. Update framework-specific sections in `.kiro/steering/project.md` before your first feature PR.

---

## Review priorities

Flag issues in this order:

1. **Security** — secrets, auth bypass, injection, unsafe client-side data exposure
2. **Correctness** — logic bugs, race conditions, missing error handling, broken async flows
3. **Regression risk** — changes without tests on non-trivial logic
4. **Maintainability** — unclear naming, dead code, over-abstraction, missing docs for public APIs
5. **Style** — only when ESLint/Prettier would not already catch it in CI

Do not nitpick formatting that CI enforces. Focus on issues a linter cannot see.

---

## TypeScript

- Flag new `any`, unchecked `as` casts, and `@ts-ignore` / `@ts-expect-error` without a comment explaining why.
- Prefer explicit return types on exported functions and public module APIs.
- Ensure `null` / `undefined` are handled at boundaries (API responses, form input, URL params).
- Flag unused variables, unreachable code, and imports that suggest incomplete refactors.

---

## React / UI (when applicable)

- **Hooks:** missing dependency arrays, stale closures, effects without cleanup (subscriptions, timers, listeners).
- **State:** derived state stored redundantly; state updates that should be functional updaters.
- **Keys:** list items rendered without stable keys; using array index as key when list order can change.
- **Accessibility:** interactive elements without labels; missing `alt` on meaningful images; keyboard traps.
- **Performance:** only flag obvious issues (e.g. new object/function in render causing unnecessary child re-renders on hot paths) — do not require premature memoization.

Update this section if the project uses a different UI library (Vue, Svelte, etc.).

---

## API routes & server code (when applicable)

Applies to Next.js App Router route handlers, API routes, Express/Fastify handlers, server actions, etc.

- **Auth:** every mutating or sensitive read endpoint must verify the caller is authorized — not just authenticated.
- **Input validation:** validate and sanitize all external input (body, query, headers, path params). Reject unexpected shapes early.
- **Secrets:** never log tokens, passwords, or API keys. Never return secrets in responses.
- **Errors:** do not leak stack traces or internal paths to clients in production responses.
- **Idempotency:** flag duplicate-submit risks on payment, enrollment, or other side-effect endpoints.

---

## Security (all web projects)

Always flag:

- Hardcoded credentials, API keys, or tokens (including in comments or test fixtures committed to the repo).
- Secrets or PII written to client bundles, `localStorage`, or URL query strings.
- `dangerouslySetInnerHTML` or equivalent without a documented sanitization strategy.
- Open redirects (`window.location = userInput`).
- SQL/NoSQL/command injection via string concatenation instead of parameterized queries.
- Missing CSRF protection on cookie-based session mutations (when applicable).
- Dependency changes that introduce known-vulnerable packages (call out the package and severity).

Reference `docs/setup.md` for how this project manages secrets (env vars, 1Password, GitHub Secrets).

---

## Testing

- **Require tests** for new business logic, utilities, reducers, validators, and API handlers — unless the PR author explains in the PR why tests are not practical.
- Flag PRs that change behavior but only update snapshots without explaining why.
- Prefer testing behavior and edge cases over implementation details.
- Mock external services in unit tests; do not call production APIs from tests.

Test command: `npm test` (must pass in CI before merge).

---

## Documentation

Flag when a PR should update docs but does not:

| Change type | Expected doc update |
|-------------|-------------------|
| New env var or config | `docs/setup.md`, `.env.example` |
| New module or architectural boundary | `docs/architecture.md` |
| User-facing behavior change | README and/or `CHANGELOG.md` |
| New API endpoint or contract | `docs/architecture.md` or inline OpenAPI/comments |

---

## AI-generated code — extra scrutiny

Many EML PRs are AI-assisted. Pay extra attention to:

- **Plausible but wrong** code — correct syntax, wrong domain logic.
- **Hallucinated APIs** — imports from packages or modules that do not exist.
- **Over-engineering** — unnecessary abstractions, generic utilities used once, excessive error-handling layers.
- **Incomplete wiring** — new UI with no route, new route with no auth, new env var not in `.env.example`.
- **Copy-paste drift** — duplicated logic that should share a helper; inconsistent naming from multiple agent sessions.
- **Missing edge cases** — empty arrays, loading/error states, network failures, permission denied.

If the PR template's **AI disclosure** is checked, verify the author listed what they tested manually.

---

## Out of scope — do not flag

- Lockfile-only changes (`package-lock.json`) unless a dependency is clearly malicious or unnecessary.
- Generated bundles, build output, `node_modules/`.
- Formatting-only diffs that CI already enforces.
- Subjective naming preferences when names are consistent with surrounding code.
- Missing tests on trivial one-line fixes (typos, comment updates, pure config for CI).

---

## Project-specific rules

<!-- Add rules unique to this project below. Examples: -->

<!-- - All WebXR session cleanup must call `session.end()` in a `finally` block. -->
<!-- - API responses must use the shared `ApiResponse<T>` wrapper in `src/lib/api.ts`. -->
<!-- - Do not add new dependencies without a GitHub issue discussing the choice. -->

---

## References

- Review skill: `.kiro/skills/eml-code-review/SKILL.md` — invoke with `/eml-code-review`
- Project conventions: `.kiro/steering/project.md`
- Lab standards: [EML AI Coding Standards](https://github.com/UBC-Emerging-Media-Lab/eml-ai-coding-standards)
- Reviewer guide: `templates/reviewer-guide.md` in the standards repo
