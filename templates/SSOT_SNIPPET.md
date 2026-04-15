<!-- Paste into AGENTS.md, CLAUDE.md, or project root agent instructions. Adjust paths. -->

## Documentation (AI-oriented)

- **Index (start here):** `docs/AI_INDEX.md`
- **Single source of truth priority:** (1) source code and generated schemas (2) tests (3) `docs/` for intent, boundaries, and decisions — not duplicated field-by-field API listings unless no schema exists.
- **On conflict:** Prefer code/schema; mark prose as stale or fix in the same task.
- **Secrets:** Never store tokens, passwords, private keys, or production connection strings in `docs/`.
