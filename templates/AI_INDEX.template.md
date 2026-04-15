# AI documentation index

Single entry point for coding agents and humans. Keep this file short; link out for detail.

## Read order (first session)

1. This file
2. [System shape](SYSTEM_SHAPE.md) (or your equivalent)
3. [Contracts](CONTRACTS.md) (or link to OpenAPI/Proto/schema)
4. [Decisions](decisions/README.md) (ADR index)

## Map

| Area        | Path | One-line purpose |
|------------|------|------------------|
| (example)  | `src/...` | ... |

## Contracts and machine-readable sources

| Kind   | Source of truth | Human notes (if any) |
|--------|------------------|----------------------|
| HTTP   | `path/to/openapi.yaml` | ... |
| Events | `path/to/schema` | ... |

## Where to change what

| If you are changing... | Update... |
|------------------------|-----------|
| Cross-package boundaries | System shape + index |
| Public API or error semantics | Contracts + ADR if breaking |

## Last aligned (optional)

Rough scope the prose matches (avoid silent drift): e.g. `src/foo` as of commit / date — update when you touch those areas.
