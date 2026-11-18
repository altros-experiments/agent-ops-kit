---
name: pr-description
description: Write a clear pull request title and description from the current branch's changes.
---

# pr-description

## Steps
1. `git log --oneline <base>..HEAD` and `git diff --stat <base>...HEAD`; read the diff.
2. Identify the user-visible change, the reason, and the risk.
3. Find linked issue numbers in branch name or commits.

## Output
```
Title: <type>(<scope>): <imperative summary, <=72 chars>

## What
<1-3 sentences, user-visible effect>

## Why
<problem or issue link: Fixes #123>

## How
- <key implementation points a reviewer needs>

## Risk & rollout
<what could break, migration/flag notes, how to roll back>

## Testing
- <commands run and results; manual steps>
```

## Rules
- Describe what the code does, not what you intended. Verify against the diff.
- No marketing words. No "this PR". Keep under 250 words unless the change is large.
