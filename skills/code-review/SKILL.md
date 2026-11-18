---
name: code-review
description: Review a diff or PR for correctness, safety and maintainability; output prioritized, actionable findings.
---

# code-review

## When to use
User asks to review a PR, branch, commit range, or staged changes.

## Steps
1. Get the diff: `git diff <base>...HEAD` (or `gh pr diff <n>`). Read the PR description/issue for intent.
2. For each changed file, read enough surrounding code to understand callers and invariants. Do not review a hunk in isolation.
3. Check in this order, stopping to note findings:
   - **Correctness:** off-by-one, null/undefined paths, wrong conditions, missing awaits, race conditions, error paths.
   - **Security:** injection (SQL, shell, path), authz checks on new endpoints, secrets in code/logs, unsafe deserialization.
   - **Data:** migrations reversible? backfills safe on large tables? transactions where needed?
   - **Tests:** does a test fail without this change? edge cases covered?
   - **Maintainability:** naming, duplication, dead code, overly clever code.
4. Run the project's checks if you can (see AGENTS.md). Note results.

## Output format
```
Verdict: approve | request changes | comment
Blocking:
- file:line: problem. Why it matters. Suggested fix.
Non-blocking:
- file:line: suggestion.
Questions:
- ...
Checks run: <commands + pass/fail>
```

## Rules
- Every finding cites file:line and proposes a concrete fix. No vague "consider refactoring".
- Separate blocking from taste. Max 5 non-blocking nits.
- If the diff is too large (>800 lines), say so and review the riskiest files first.
