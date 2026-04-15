---
name: ai-project-context
description: Use when working in large or multi-module repos, changing public APIs, cross-package boundaries, data ownership, or adding/removing services; when durable orientation docs would help future agent sessions; when prior prose may be stale relative to code
---

# AI project context (layered docs)

## Overview

Maintain **small, layered Markdown** so new coding-agent sessions can orient fast without rereading the whole tree. Docs complement code, tests, and schemas; they do not replace them.

**Core principle:** Index first, layered truth, same-task updates, no silent drift.

**Violating the letter of a rule below is violating its spirit.**

## When to use

- Multiple packages, services, or ownership boundaries.
- Changes that alter what callers may assume (public API, errors, events, persistence).
- New infrastructure others must discover (queues, feature flags, migrations policy).
- You are the one who knows *why* a boundary exists; the next session will not.

## When not to use

- Single-file scripts or throwaway spikes (skip heavy process).
- Pure internal refactor with identical external behavior (code/comments/tests suffice).
- Information already guaranteed by a generated schema and navigation is trivial (link only; do not duplicate fields).

## Documentation layers

Use stable names your repo declares (see project `AGENTS.md` / `CLAUDE.md` + SSOT snippet). Typical layers:

| Layer | Role | Allowed | Forbidden |
|-------|------|---------|-----------|
| **A — Index** | One entry point, links only | Short map, read order, pointers to contracts | Long prose, full API listings copied from schema |
| **B — System shape** | Boundaries, data ownership, dependency direction | Boxes/arrows, invariants, “who calls whom” at module level | Class-by-class walkthroughs |
| **C — Contracts** | External promises | Link to OpenAPI/Proto/JSON Schema; semantic notes tests cannot carry | Hand-maintained field tables when a generator owns the schema |
| **D — ADRs** | Irreversible or expensive choices | Context, decision, consequences, links | Implementation diaries |
| **E — Runbook (optional)** | How to run, env quirks | Commands, local URLs (non-secret) | Production secrets |

## Change-type matrix

| Change | Touch layers | Code-only OK? |
|--------|--------------|----------------|
| Cross-module dependency direction | A, B | No |
| Public API / error semantics / events | A, C; ADR if breaking | No |
| Data model visible outside owning module | B, C; ADR if migration policy shifts | No |
| New service or top-level package | A, B | No |
| Internal refactor, same behavior | — | Yes |
| Config exists only in secret store | E mentions *name* of secret, not value | N/A |

If unsure, update **A** at least (one line + link).

## Single source of truth (SSOT)

Default precedence (project may restate in SSOT snippet):

1. Source code and generated artifacts (OpenAPI, protos, types).
2. Automated tests for behavior contracts.
3. Markdown for **intent**, **boundaries**, and **decisions** not obvious from (1)(2).

**On conflict:** Prefer (1)(2). Either fix prose in the **same task** or mark it stale with a visible note (date/scope) — never leave authoritative-sounding wrong text.

## Lifecycle

- **Create:** From templates; prefer empty sections over invented detail.
- **Update:** In the **same agent task / PR** as the code change when matrix says so.
- **Deprecate:** Mark deprecated, link successor; remove dead links from A.
- **Archive:** Move superseded long text to `docs/archive/`; keep A lean.

Deleting code or a public endpoint **must** update or explicitly retire related doc sections in the same change.

## Security (hard rules)

Never write to `docs/` (or any committed file): tokens, passwords, private keys, production connection strings, customer identifiers, or raw production logs. Use placeholders and point to secret managers. Examples must be synthetic.

## Division of labor vs project files

- This skill: **when**, **what layer**, **how little**, **what is forbidden**.
- Project files (`AGENTS.md`, `CLAUDE.md`, etc.): **exact paths** (e.g. `docs/AI_INDEX.md`), naming, team quirks.

Copy `templates/SSOT_SNIPPET.md` into the project and adjust paths.

## Anti-patterns

- Dumping `tree` output as “documentation”.
- One megabyte README that tries to be A+B+C+D.
- Duplicating API fields by hand alongside a generated schema.
- Putting “notes for the AI” in **user-visible UI copy** — keep agent guidance in `docs/` or agent config.
- “Always update docs every commit” without the matrix — causes noise and new drift.

## Verification (skill quality)

Before treating this discipline as “working” in a repo, run a few **pressure scenarios** (with and without this skill loaded): API change without C; new package without A; internal refactor that incorrectly rewrites B; accidental secret in a doc; prose contradicting an ADR. Tighten project rules where the agent rationalizes skipping updates.

## Quick gate

Before ending a task that hit the matrix:

1. **IDENTIFY** — Which layers were affected?
2. **UPDATE or RETIRE** — Same change; no silent drift.
3. **SCAN** — No secrets; no duplicated schema; index links still valid.

Skip only when the matrix says code-only is enough.
