---
inclusion: always
---

# Code search and context discipline

Prefer Kiro's built-in tools over dumping whole files or generic terminal search:

1. Use Kiro's code-reading and search tools (structured/AST-aware code reading, grep, and file search) to locate symbols and references.
2. Read only the line ranges you need. Reserve full-file reads for small files (under ~100 lines) or when editing a whole module.
3. Do not paste large generated assets, lockfiles, or build output into chat.

## Paths agents should skip

Agents honor `.gitignore`. In addition, do not read or edit these unless a task explicitly requires it:

- `node_modules/`, `dist/`, `build/`, `.next/`, `out/`, `.cache/`, `coverage/`
- `.env`, `.env.local`, `.env.*.local` (secrets — never read or echo values)
- Source maps (`*.map`), large media in `public/` (`*.mp4`, `*.glb`)
- Tool caches (`.turbo/`, `.vercel/`)
