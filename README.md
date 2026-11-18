# Agent Ops Kit (free edition)

Drop-in **AGENTS.md** templates and **SKILL.md** skills that make AI coding agents (Claude Code, Codex CLI, Cursor, Copilot agent, OpenClaw, Aider) work like a careful senior engineer: they run your checks before saying "done", keep diffs scoped, write real tests, and ask before destructive actions.

## Free in this repo
- `agents-md/typescript-node.AGENTS.md`: a production AGENTS.md template
- `skills/code-review`: prioritized, file:line review findings
- `skills/pr-description`: PR titles and descriptions from your diff
- `skills/bug-repro`: turns a bug report into a failing test first
- `guardrails/GUARDRAILS.md`: safety rules, permission tiers, secret hygiene

## Use it
1. Copy `agents-md/typescript-node.AGENTS.md` to your repo root as `AGENTS.md` (and `CLAUDE.md` for Claude Code). Edit the commands.
2. Copy skills into `.claude/skills/` (Claude Code), `skills/` (OpenClaw), or `.agents/skills/`.
3. Ask: *"Review my staged changes using the code-review skill."*

## Full kit: $19
The [full Agent Ops Kit](https://emperoraltros.gumroad.com/l/agent-ops-kit) adds:
- 4 more AGENTS.md templates: **Python, Go, Monorepo, Docs site**
- 9 more skills: **test-writer, dependency-upgrade, migration-safety, refactor-plan, release-notes, incident-postmortem, api-design-review, security-checklist, perf-triage**
- A quickstart for every major agent tool

👉 **[Get the full kit](https://emperoraltros.gumroad.com/l/agent-ops-kit)**

## Contributing
Issues and PRs with improvements are welcome.

_Written with AI assistance, then reviewed and tested._
