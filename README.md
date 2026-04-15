# ai-project-context-skill

A standalone **[Agent Skill](https://agentskills.io/specification)** that helps coding agents maintain **layered, low-drift Markdown** in real repositories: an index, system shape, contracts (as links to schemas where possible), and ADRs—without replacing code, tests, or generated API artifacts.

**Relationship to [Superpowers](https://github.com/obra/superpowers)-style workflows:** Superpowers emphasizes process (plans, TDD, verification). This skill emphasizes **durable, retrievable context** (where to look, what must stay true, what changed). They complement each other.

## Contents

| Path | Purpose |
|------|---------|
| [skills/ai-project-context/SKILL.md](skills/ai-project-context/SKILL.md) | The skill: triggers, layers, matrix, SSOT, lifecycle, security |
| [templates/AI_INDEX.template.md](templates/AI_INDEX.template.md) | Starter index for `docs/AI_INDEX.md` |
| [templates/ADR.template.md](templates/ADR.template.md) | ADR skeleton |
| [templates/SSOT_SNIPPET.md](templates/SSOT_SNIPPET.md) | Paste into `AGENTS.md` / `CLAUDE.md` with your paths |

## Install (copy the skill folder)

Client paths change over time—**verify against your product’s current docs**. Typical patterns:

### Cursor

- Copy the directory `skills/ai-project-context/` into the location your Cursor version uses for **project** or **user** skills (often under `.cursor/` in the repo or in your user config directory for skills).  
- See Cursor documentation for **Skills** / **Rules** layout for your release.

### Claude Code

- Copy `skills/ai-project-context/` into your Claude Code skills directory (e.g. user-level skills path described in Claude Code docs).

### Other agents

- Any client that loads `SKILL.md` with YAML frontmatter per [agentskills.io](https://agentskills.io/specification) can use the same folder as-is.

## Use in a business repository

1. Copy templates from `templates/` into your repo (e.g. `docs/AI_INDEX.md` from `AI_INDEX.template.md`).
2. Add a short **SSOT** block to `AGENTS.md`, `CLAUDE.md`, or equivalent—start from [templates/SSOT_SNIPPET.md](templates/SSOT_SNIPPET.md) and set real paths.
3. Keep **layer A** (index) small; link to schemas instead of copying them.
4. Optional coarse CI (not included here): e.g. require `docs/AI_INDEX.md` for certain labels—add your own policy if needed.

## Security

- **Never** commit PATs, passwords, or private keys. `.gitignore` in this repo lists common patterns; extend it in your own repo as needed.
- Prefer **`gh auth login`** or **SSH keys** for GitHub; keep credentials out of the tree.

## GitHub authentication (appendix)

- **Push / `gh`:** In the integrated terminal, run `gh auth login` and follow prompts, or use SSH remotes with an agent-loaded key.
- **Cursor ↔ GitHub account linking:** Use Cursor’s Settings → account / integrations per your app version; see [Cursor documentation](https://docs.cursor.com).

## License

MIT — see [LICENSE](LICENSE).
