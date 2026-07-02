# <PROJECT_NAME> — Agent Operating Manual

<!-- POPULATE: replace all <PLACEHOLDERS>. This file is the single entry point for ANY agent harness. Keep it lean; detail lives in referenced files. -->

**Project:** <PROJECT_NAME> — <ONE_LINE_DESCRIPTION>
**Stack pack:** `stacks/<web-app|api-service|mobile-app>.md`
**Constitution:** `constitution.md` (non-negotiable — read before any work)

## Prime directives

1. **Spec first.** No implementation without an approved spec in `specs/`. If asked to build without one, run the spec workflow (`prompts/spec.md`) first.
2. **Cheapest capable model.** Work is tiered Plan / Build / Scout per `agents/routing.md`. Use the lowest tier capable of the task.
3. **Maintainability over cleverness.** Code must be extensible by any agent or human. Follow `standards/engineering-standards.md` exactly.
4. **Small, verifiable steps.** One task from `tasks.md` at a time; tests must pass before the next.
5. **Never touch protected paths** (see `guardrails/protected-paths.txt`, enforced by pre-commit + CI): `.env*`, `secrets/`, approved specs, lockfiles, `constitution.md`, guardrail and agent configs.

## Roles

Adopt the role that matches the work; role cards live in `agents/`:

| Role | Tier | Work |
|---|---|---|
| architect | Plan | Specs, plans, task breakdowns, ADRs |
| reviewer | Plan | Merge-gate review vs spec + constitution (blocking) |
| security-auditor | Plan | Security review of every gated diff |
| implementer | Build | Production code, one task at a time |
| test-engineer | Build | Acceptance + regression tests |
| devops | Build | CI/CD, IaC, deploys per `pipeline/sdlc-playbook.md` |
| scout | Scout | All codebase search/reconnaissance |
| doc-writer | Scout | Docs, changelogs, doc comments |

If your harness supports sub-agents/modes, register these per your `adapters/` guide; otherwise prepend the role card to your prompt.

## Workflow

1. `prompts/spec.md` → `specs/NNN-slug/spec.md` (EARS). Human approves.
2. `prompts/plan.md` → `plan.md` (+ ADRs). Human approves.
3. `prompts/tasks.md` → `tasks.md` (atomic, tiered, testable). Human approves.
4. `prompts/implement.md` → code + tests, task by task.
5. Review gate: reviewer + security-auditor verdicts on the diff. Both must APPROVE.
6. `pipeline/` deploys; post-deploy verification per stack pack.

## Context economy

- Scout-tier work for all searching/reading reconnaissance; return conclusions, not file dumps.
- Grep before read; read sections, not whole files.
- Between features, clear/compact context — stale context is a token tax.

## Standards (load only when doing the relevant work)

`standards/engineering-standards.md` · `standards/testing-standards.md` · `standards/security-baseline.md` · `standards/design-primer.md`

## Project specifics

<!-- POPULATE -->
- Language/runtime: <LANG_RUNTIME>
- Build: `<BUILD_CMD>` · Test: `<TEST_CMD>` · Lint: `<LINT_CMD>` · Typecheck: `<TYPECHECK_CMD>`
- Run locally: `<DEV_CMD>`
- Deploy target: <DEPLOY_TARGET>
