# Guardrails — Portable Enforcement

Harness hooks aren't portable, so enforcement lives in three layers that work no matter which tool wrote the code:

| Layer | Mechanism | Catches |
|---|---|---|
| 1. Instructions | `AGENTS.md` prime directives + role access limits | Most violations, cheaply — but advisory only |
| 2. Local hard stop | `guardrails/pre-commit` git hook | Protected-path changes and secrets before they enter history |
| 3. Remote hard stop | `pipeline/ci/` (branch protection + required checks) | Everything layer 2 catches (agents can skip local hooks) + tests, coverage, dep audit, spec traceability |

Layer 3 is the one that cannot be bypassed: enable branch protection requiring the CI job, and no direct pushes to main.

## Protected paths

Machine-readable list: `protected-paths.txt` (one regex per line; used by the pre-commit hook and CI). Human-readable intent:

- `.env*`, `secrets/` — secrets never enter history or agent context.
- Lockfiles — dependency changes go through ADR + human application.
- `constitution.md`, `AGENTS.md`, `guardrails/`, `agents/`, harness config dirs (`.claude/`, `.github/copilot*`, `.cursor/`, etc.) — the enforcement layer must not be editable by the thing it constrains.
- `specs/**/spec.md` with `status: approved` — immutable; amend via revision bump + re-approval.

## Harness-native hooks (optional hardening)

Where the harness supports pre-action hooks (Claude Code today), wire layer-2 checks there too so violations are blocked *before* the edit, not at commit. See `adapters/claude-code.md`. For other harnesses, layers 2+3 suffice.

## Changing guardrails

Human-only, via ADR. An agent may propose a diff in a scratch file; a human applies it.
