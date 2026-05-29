# AGENTS.md

> Global coding agent rules — Hermes Edition
> Forked and remixed from [zeke/agents.md](https://github.com/zeke/agents.md)
> Persona lives in `~/.hermes/SOUL.md`. This file is for project and engineering rules only.

---

## Working with me

- Be direct. No glazing. Never open with "You're absolutely right!" or similar sycophantic openers.
- Push back with specific reasons when you disagree. If it's a gut feeling, say so.
- If you don't know something (env vars, API endpoints, CLI flags, model names, library APIs), stop and verify or say you don't know. Never invent technical details.
- Your training data is stale. Verify model names, package versions, and API surfaces before relying on them.
- Don't say a task is done until typechecks, linters, and tests pass. If none are configured, say so explicitly instead of claiming success.
- When renaming a function, type, or variable, search separately for: direct references, type-level references, string literals containing the name, dynamic imports, re-exports and barrel files, and test or mock files. One grep is not enough.

---

## Before coding

- State assumptions explicitly before implementing. If uncertain, ask.
- If multiple interpretations of a request exist, present them — don't pick silently.
- If something is unclear, name what's confusing instead of guessing.
- Write the minimum code that solves the problem. No speculative features, no abstractions for single-use code, no configurability that wasn't asked for.
- Don't add error handling for impossible scenarios.
- Touch only what the task requires. Don't improve adjacent code, comments, or formatting.
- Match existing style in a file, even if you'd write it differently.
- If you notice unrelated dead code or bugs, mention them — don't fix them unprompted.
- Clean up orphans your changes create (unused imports, variables). Don't remove pre-existing dead code unless asked.

---

## Reasoning before acting

Before any non-trivial change, run this protocol internally:

1. What is actually being asked? (restate it in one line)
2. What assumptions must be true for this to work?
3. What are the risks — what could break, regress, or cause future pain?
4. What is the simplest correct path?
5. Execute, then verify the result is correct before moving on.

If you skip this and something breaks, that's on you.

---

## Atomic task decomposition

Before any significant change:

- Break work into 10-15 small, specific tasks — not 4-5 vague ones.
- Each task should be completable in a single focused change.
- Track internally if possible. If the task is complex, create `todos.txt` at project root. Delete it when done.
- Format:
  ```
  - [ ] Task 1: specific atomic action
  - [ ] Task 2: specific atomic action
  ```

---

## Running scripts and commands

- Use GitHub's "Scripts to Rule Them All" approach: https://github.com/github/scripts-to-rule-them-all
- If the project has a `scripts/` or `script/` directory, run those scripts for testing, linting, formatting.
- If a `script/lint` or `scripts/lint` script exists, run it before committing.
- If linting fails, fix and re-run until clean. Do not commit with lint errors.

---

## Working with Git

- Always use semantic commit prefixes (`feat:`, `fix:`, `chore:`, `docs:`, `refactor:`, `test:`), with or without parenthetical qualifiers.
- PR/MR titles must use semantic commit format.
- Never bypass pre-commit hooks. Never use `--no-verify` without explicit permission.
- **NEVER push to main or the default branch. Always push to a feature branch.**
- Don't push commits to branches with PRs that have already been merged.

---

## Working with Node.js and npm

- Always use `npx` when running global npm CLIs (e.g. `npx wrangler` not `wrangler`).
- Match the existing package manager of the project (npm/pnpm/yarn). Never mix.

---

## Working with Cloudflare

- Always use JSONC for Workers configs (not TOML).
- Use `.env` files for secrets. Don't use `.dev.vars` — it's Cloudflare-specific and non-portable.
- Always use the latest versions of Wrangler and Cloudflare npm packages.
- Prefer API/CLI over the Cloudflare dashboard.
- Favor Cloudflare Workers over Pages for non-static workloads.
- Use Hono for worker apps when appropriate.

---

## Working with GitHub and GitLab

- Use `gh` for GitHub repositories, `glab` for GitLab.
- When writing a PR/MR body: concise, explain the problem and solution. Start with "This PR..."
- No "Summary" heading. No test plan mentions.
- Don't use: "comprehensive", "seamlessly", "utilize", "implement", "exhaustive".
- Read all comments and discussion threads when analyzing issues/PRs/MRs. Context lives in the conversation.
- After creating or updating a PR/MR or issue, open the URL in the default browser.
- When creating a new GitHub repo with `gh repo create`, set `--homepage` and `--description` if context allows.

---

## Style guide

- Concise and descriptive in all written output.
- No em dashes (—). Use commas, colons, or separate sentences.
- No bold in markdown prose.
- Avoid headings smaller than H2 in markdown.
- Pad markdown table cells with spaces so columns align in monospace.
- Comments explain WHY, not WHAT:
  ```
  // WRONG: Loop through users and filter active ones
  // CORRECT: In-memory filter because user list is already loaded — avoids extra DB round-trip.
  ```

---

## Types and documentation

- Prefer types over prose for API contracts. Types can't drift from implementation.
- Define Zod schemas as single source of truth, then derive TypeScript types and OpenAPI specs from them.
- Reserve prose docs for explaining *why* a system exists and *when* to use it — not *what* it accepts.
- If an API is too complex to type cleanly, that's a design problem worth fixing.

---

## Fetching data

- If a public page returns 403, try alternate methods (different headers, cached versions, alternate sources).
- Never fabricate data from a failed fetch. Flag the failure, ask for direction.

---

## Browser automation

- Use https://agent-browser.dev (`agent-browser` CLI) or https://github.com/andreasjansson/plwr (`plwr` CLI).
- Prefer CLI tools over MCP servers for browser tasks.
- Don't use browser automation for tasks achievable via API or CLI.
- Never navigate away from or overtake unrelated existing browser tabs.

---

## Secrets and credentials

- NEVER hardcode API keys, tokens, passwords, or secrets in source code.
- Always read secrets from environment variables.
- Before committing, scan staged changes for secrets. If found, stop and flag.
- Secrets belong in `.env` files listed in `.gitignore`.
- If a secret is already committed, flag it immediately and recommend rotating it.

---

## Completion report

After any significant task:

**What**: One-line summary
**How**: Key implementation decisions
**Why**: Reasoning over alternatives
**Smells**: Tech debt, workarounds, tight coupling, unclear naming, missing tests
**Risks**: What could break, what needs monitoring, what's fragile

Bullets, no fluff. Transparent about tradeoffs.

---

## Self-improvement

- When corrected, after finishing the task, propose a one-line edit to the relevant AGENTS.md so the same mistake doesn't recur.
- Decide scope explicitly: global AGENTS.md if it applies across all projects, project `./AGENTS.md` if it only applies here.
- Before proposing, search for an existing rule that covers this. If one exists, tighten it — don't add a duplicate.
- Show the proposed diff. Do not edit until approved.
- Match surrounding style: bullet, no bold, no em dashes, concise.
- If more than two rules are suggested in one session, stop and ask if we're overcorrecting.
- When AGENTS.md grows past ~200 lines, propose deletions or consolidations alongside additions.

---

## General advice

- Prefer API/CLI over web-based workflows wherever possible.
- Finish messages with a list of relevant URLs (pages consulted, PRs created, issues opened).
- When you overcome an obstacle or learn something generally useful, prompt to add a note to AGENTS.md so future sessions benefit.

---

## Important rules

- NEVER PUSH TO THE MAIN OR DEFAULT BRANCH. ALWAYS PUSH TO A FEATURE BRANCH.
- If your last message included HTTP/HTTPS URLs, offer to open them in the default browser.
- Don't push commits to branches with already-merged PRs.

---

*Hermes Edition — forked from [zeke/agents.md](https://github.com/zeke/agents.md) · remix freely*
