# Guardrails for AI coding agents

Paste the block below into your AGENTS.md (or CLAUDE.md) and adjust paths.

```md
## Safety rules (always apply)
- Ask before any destructive or irreversible action: deleting files or branches, force-pushing,
  dropping tables, running migrations, rotating keys, publishing packages, sending messages or emails.
- Prefer reversible operations: move to trash instead of delete, new branch instead of rewriting history.
- Never print, log, commit or paste secrets. If you see one, stop and tell the user where it is.
- Stay inside the repository. Do not read or write files outside it unless explicitly asked.
- Network: only fetch documentation or package registries needed for the task.
- If the same command fails 3 times, stop and report instead of trying variations.
- Never claim "done" without running the project's checks. Paste the summary of their output.
```

## Permission tiers (copy into your agent tool config)

| Tier | Examples | Policy |
|---|---|---|
| Read | ls, cat, grep, git status/diff/log | Always allowed |
| Local write | edit files in repo, run tests/linters, git commit on a feature branch | Allowed |
| Shared write | git push, open PR, comment on issues | Allowed on feature branches; ask for default branch |
| Destructive | rm -rf, git push --force, reset --hard, DB drop/migrate, deploy | Always ask |
| External | email, chat messages, payments, publishing | Always ask, show exact content first |

## Secret hygiene checklist
- [ ] `.gitignore` covers `.env*`, `*.pem`, `*.key`, credential JSON files
- [ ] A pre-commit secret scanner (gitleaks or trufflehog) is installed
- [ ] Agent tool output that may contain secrets is not echoed back into chat
- [ ] Tokens given to agents are fine-grained, scoped to one repo/org, and expire

## Review checklist for agent-written PRs
- [ ] Diff touches only files related to the task
- [ ] Tests were added or updated and actually exercise the change
- [ ] No disabled tests, no new `// eslint-disable`, `# type: ignore`, `nolint` without a reason
- [ ] No new dependencies the task did not need
- [ ] Error paths handled, not swallowed
