# SDLC Playbook — Phase Gates

Every feature moves through these phases. A phase's exit gate must pass before the next begins. Gates marked 🧑 require a human.

| # | Phase | Owner (tier) | Exit gate |
|---|---|---|---|
| 0 | Intake | human + architect | Idea captured; worth a spec? 🧑 |
| 1 | Specify (`prompts/spec.md`) | architect (Plan) | EARS spec, no open questions, `status: approved` 🧑 |
| 2 | Plan (`prompts/plan.md`) | architect (Plan) | Plan + ADRs approved; constitution compliance stated 🧑 |
| 3 | Task (`prompts/tasks.md`) | architect (Plan) | Atomic tasks, tiered, cost estimate within budget 🧑 |
| 4 | Implement (`prompts/implement.md`) | implementer/test-engineer (Build), scout (Scout) | All tasks done; suite + lint + typecheck green; per-task acceptance tests pass |
| 5 | Review gate | reviewer + security-auditor (Plan) | Both `VERDICT: APPROVE`; verdicts recorded in tasks.md |
| 6 | Merge + CI | devops (Build) | Pipeline green: build, tests, coverage floor, secret scan, dep audit, a11y (UI stacks) |
| 7 | Deploy staging | devops (Build) | Post-deploy verification (stack pack) passes |
| 8 | Deploy production | devops (Build) | Staging soak OK; human approves 🧑; rollback path stated |
| 9 | Verify + close | devops + doc-writer | Prod verification green; docs/CHANGELOG updated; cost-report appended; spec `status: implemented` |

## Failure handling

- Gate fails → findings become tasks → return to phase 4 (or 1–3 if the spec/plan is wrong — fix the spec, never patch around it).
- Production incident → rollback first, diagnose second; regression test + spec amendment before re-deploy.

## Rules

- No phase skipping, including "trivial" changes — trivial changes get trivial specs (a 5-line spec is fine; no spec is not).
- Phases 1–3 may run in one session for small features, but each gate is still checked.
- Costs are logged per phase where telemetry allows; budget breach behavior per `observability/cost-policy.md`.
