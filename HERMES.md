# HERMES.md

> Project-level context for Hermes Agent.
> This file is loaded automatically by Hermes when working in this repo.
> Keep it focused on repo-specific facts: stack, commands, conventions, gotchas.

---

## What this repo is

This is a personal global `AGENTS.md` repository — a public, forkable collection of
coding agent rules and Hermes Agent configuration files.

Goal: provide a ready-to-use Hermes setup (SOUL.md + AGENTS.md + HERMES.md) that
anyone can fork, customize, and load into their own Hermes instance.

---

## File map

| File | Purpose | Where it goes |
| ----------- | -------------------------------------------- | ----------------------- |
| `SOUL.md` | Agent identity, tone, persona | `~/.hermes/SOUL.md` |
| `AGENTS.md` | Global coding rules for all projects | `~/.hermes/AGENTS.md` or project root |
| `HERMES.md` | Repo-specific context for Hermes Agent | project root |

---

## Setup instructions

```bash
# Clone the repo
git clone https://github.com/lizhouc1010-lang/agents.md.git
cd agents.md

# Install SOUL.md globally
cp SOUL.md ~/.hermes/SOUL.md

# Install AGENTS.md globally (optional — or use per-project)
cp AGENTS.md ~/.hermes/AGENTS.md

# HERMES.md stays in project root — Hermes loads it automatically
```

---

## Customization guide

- Edit `SOUL.md` to change personality, tone, directness level.
- Edit `AGENTS.md` to change engineering rules, commit style, tool preferences.
- Create a project-specific `AGENTS.md` in any repo — it overrides or extends the global one.
- Use `~/.hermes/config.yaml` to add custom `/personality` presets.

---

## Key conventions in this repo

- All markdown files use H2 as the smallest heading (no H3/H4 in prose).
- No bold text in prose sections.
- No em dashes anywhere.
- Tables have space-padded columns for monospace readability.
- Attribution to [zeke/agents.md](https://github.com/zeke/agents.md) is preserved in AGENTS.md footer.

---

## Related links

- Hermes Agent docs: https://hermes-agent.nousresearch.com/docs/
- SOUL.md guide: https://hermes-agent.nousresearch.com/docs/guides/use-soul-with-hermes
- Context files reference: https://hermes-agent.nousresearch.com/docs/user-guide/features/context-files
- Upstream fork: https://github.com/zeke/agents.md
- AGENTS.md format spec: https://agents.md
