---
name: bug-repro
description: Turn a bug report into a minimal, failing reproduction test before any fix is attempted.
---

# bug-repro

## Steps
1. Restate the bug as: given <state>, when <action>, expected <X>, actual <Y>. Ask if any part is unknown.
2. Locate the code path: search for error messages, route names, function names from the report.
3. Write the smallest failing test in the project's test framework. Name it after the behavior: `test_<thing>_<condition>_<expected>`.
4. Run it and confirm it fails **for the reported reason** (check the assertion message, not just "it failed").
5. If you cannot reproduce after 3 attempts, stop. Report what you tried and what extra info is needed (version, input, logs).

## Output
- The failing test (file path + code)
- Command to run it and the failure output
- One-paragraph root-cause hypothesis with file:line

## Rules
- Do not fix the bug in this skill unless asked. A clean repro is the deliverable.
- Prefer unit-level repro; use integration tests only if the bug lives in the wiring.
