# agents.md — Hermes Edition

My global configuration files for [Hermes Agent](https://github.com/NousResearch/hermes-agent) and other AI coding agents.



---

## Files

| File | What it is |
| ----------- | ------------------------------------------------------- |
| `SOUL.md` | Hermes Agent identity — goes in `~/.hermes/SOUL.md` |
| `AGENTS.md` | Global coding rules — works with Hermes, Claude Code, OpenCode, Cursor, Copilot |
| `HERMES.md` | Repo-specific context loaded by Hermes in this project |

---

## Quick install

```bash
git clone https://github.com/lizhouc1010-lang/agents.md.git
cd agents.md

# Load identity into Hermes
cp SOUL.md ~/.hermes/SOUL.md

# Load global rules (optional)
cp AGENTS.md ~/.hermes/AGENTS.md
```

Then restart Hermes or start a new session.

---

## How it works

Hermes Agent reads a layered set of context files every session:

```
~/.hermes/SOUL.md       ← who the agent is (identity, tone, style)
~/.hermes/AGENTS.md     ← global engineering rules
./AGENTS.md             ← project-specific rules (overrides global)
./HERMES.md             ← project-specific Hermes context
```

SOUL.md is the agent's **identity** — it goes in slot #1 of the system prompt.
AGENTS.md is for **rules** — git conventions, code style, tool preferences.
Keep them separate. Don't mix identity and project instructions.

---

## Works with any agent

AGENTS.md is read by:

- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [Claude Code](https://docs.anthropic.com/claude-code)
- [OpenCode](https://opencode.ai)
- [Cursor](https://cursor.sh)
- [GitHub Copilot](https://github.com/features/copilot)
- Any tool that supports the [AGENTS.md spec](https://agents.md)

---

## Customizing

- Change `SOUL.md` to reshape the agent's personality and communication style.
- Change `AGENTS.md` to change engineering rules, commit style, tool preferences.
- Create a project-level `AGENTS.md` in any repo for project-specific overrides.

See [Hermes Agent docs](https://hermes-agent.nousresearch.com/docs/) for full configuration reference.

---

## Credits

- [zeke/agents.md](https://github.com/zeke/agents.md) — original global AGENTS.md by Zeke Sikelianos
- [agents.md spec](https://agents.md) — open format for coding agent instructions
- [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) — the agent this is tuned for
