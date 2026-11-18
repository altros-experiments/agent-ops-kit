# AGENTS.md: TypeScript / Node service

## Project map
- `src/`: application code. `src/routes/` = HTTP handlers, `src/lib/` = pure logic, `src/db/` = data access.
- `test/`: tests mirror `src/` paths. Fixtures live in `test/fixtures/`.
- Generated code: `src/gen/`. Never hand-edit; regenerate with `npm run gen`.

## Commands (run before claiming done)
- Install: `npm ci` (never `npm install` in CI-like runs; it rewrites the lockfile)
- Typecheck: `npm run typecheck`
- Lint: `npm run lint -- --max-warnings=0`
- Test one file: `npx vitest run path/to/file.test.ts`
- Full suite: `npm test`

## Conventions
- Strict TypeScript. No `any`; use `unknown` + narrowing. No non-null `!` unless commented why.
- Errors: throw typed errors from `src/lib/errors.ts`; handlers map them to status codes. Never swallow errors.
- Logging: `logger` from `src/lib/log.ts`, structured fields, no secrets or tokens in logs.
- Async: always `await` or return promises; no floating promises.
- Dependencies: ask before adding a runtime dependency. Dev dependencies are fine with a one-line reason in the PR.

## Done means
1. Typecheck, lint and the relevant tests pass locally (paste the command output summary).
2. New behavior has a test that fails without the change.
3. No unrelated files changed. No formatting-only churn.
4. Public API or env var changes are reflected in README.

## Never
- Commit `.env*`, credentials, or real customer data.
- Run migrations against anything but the local DB.
- Disable a failing test to get green; fix it or report it.
