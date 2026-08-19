# Factory Bridge Reality Report

Date: 2026-08-19

## Final finding

`PARTIAL`

The Codex Bridge genuinely invokes the Factory-owned executor. A prior local
smoke completed the real Worker, Factory submit, acceptance gates, and
Controller-owned Git commit. It was not a READY-only handoff.

The successful Worker trajectory did not issue `factory ask-gemini`. Therefore
the Dispatcher seam was wired but not exercised, and the Gemini Web Provider
was not called in that run.

## Requested checks

| Check | Result | Evidence |
|---|---|---|
| Codex Bridge calls executor | PASS | `factory_codex_calls_executor=PASS`; executor status `complete` |
| WorkOrder enters dispatcher | NOT REACHED | successful intercepted command list contains only `submit` |
| Worker starts | PASS | North Worker, exit status `Submitted`, 22 trajectory messages |
| Worker Provider call | PASS | 10 model API calls in trajectory; OpenRouter/North Worker completed |
| Gemini Provider call | NOT REACHED | no `factory ask-gemini` action |
| Factory submit | PASS | `submit` intercepted; Controller status `done` |
| Git commit | PASS | result SHA present; tested SHA equals result SHA |

## Current environment blocker

A fresh live rerun is not currently reproducible from this process:

- `OPENROUTER_API_KEY` is missing from the Factory process.
- The protected Gemini Web API endpoint returns HTTP 401 unauthorized.
- Docker Desktop Linux daemon is unavailable.

The local executor itself is intentionally Docker-free, so Docker does not
invalidate the historical local smoke. It does block the separate Docker
execution path.

## Next precise validation

Configure the Worker credential and the Factory-side Gemini Web proxy auth,
then run a task whose Worker must issue `factory ask-gemini` before submit.
The required expected command sequence is:

`factory ask-gemini -> submit`

Only that run can mark Dispatcher and Gemini Provider as PASS.
