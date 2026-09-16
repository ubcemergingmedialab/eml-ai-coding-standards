# EML review checklist (condensed)

Use when `.kiro/REVIEW.md` is missing. Prefer reading `.kiro/REVIEW.md` in project repos.

## Security

- [ ] No secrets, tokens, or PII in code, comments, tests, or client bundles
- [ ] Auth on mutating/sensitive server endpoints
- [ ] Input validation on external data
- [ ] No `dangerouslySetInnerHTML` without sanitization
- [ ] New env vars in `.env.example` and `docs/setup.md`

## Correctness

- [ ] Null/undefined handled at boundaries
- [ ] Async errors caught; no unhandled promise rejections
- [ ] React: effect cleanup, stable list keys, no obvious stale closures
- [ ] No hallucinated imports or APIs

## Tests & CI

- [ ] Non-trivial logic has tests (or PR explains why not)
- [ ] `npm run lint`, `npm test`, `npm run build` expected to pass

## Spec compliance

- [ ] Change matches linked GitHub issue acceptance criteria
- [ ] No out-of-scope work (or split to separate issue)

## AI-generated code

- [ ] No over-engineering or incomplete wiring (route without auth, UI without handler)
- [ ] Author verified behavior manually (check PR AI disclosure)

## Documentation

- [ ] README / `docs/architecture.md` / `docs/setup.md` updated when behavior or setup changes

## Out of scope — skip

- Formatting CI enforces
- Lockfile-only changes (unless dependency is suspicious)
- Trivial one-line fixes without logic changes
