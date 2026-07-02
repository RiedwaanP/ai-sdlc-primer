# Source Control & Deploy-from-GitHub Strategy

GitHub is the system of record: all work lands there via PR, and all deploys originate from it. Nothing deploys from a laptop.

## Branching (trunk-based, spec-scoped)

- `main` is always releasable (Constitution Art. II) and is the only long-lived branch.
- One branch per spec: `spec/NNN-slug` (e.g. `spec/001-record-detect-key`). Short-lived — merged when the review gate passes, then deleted.
- Sub-branches only for `[P]` parallel agent work, merged back into the spec branch, never directly to main.

## Commits

- Conventional commits with spec/task traceability: `feat(scope): summary [Spec NNN][T-00X]` (also `fix`, `test`, `docs`, `refactor`, `chore`).
- One task = one commit (or a few coherent ones). Agents commit after each completed task, not in end-of-session batches.
- Never commit: secrets, generated artifacts, `.env*` (guardrails/pre-commit + CI enforce).

## Pull requests

- One PR per spec, from `spec/NNN-slug` → `main`; title references the spec (`Spec 001: record → detect key`) — CI enforces this.
- PR body: requirements satisfied, review-gate verdicts (reviewer + security-auditor), escalations, cost summary.
- Branch protection on `main` (set once, human-owned): require the CI check, require PR (no direct pushes), no force-push. This is the unbypassable enforcement layer.

## Deployment (from GitHub only)

- **Staging:** merge to `main` → CI green → auto-deploy to staging → post-deploy verification (stack pack).
- **Production:** human-triggered GitHub Actions release workflow (tag `vX.Y.Z` or environment approval gate) — this is the Constitution Art. VI human control point, recorded in the workflow run.
- Use GitHub Environments (`staging`, `production`) with required reviewers on `production`; secrets live in environment secrets, never in the repo.
- **Rollback:** re-deploy the previous tag (preferred) or `git revert` the offending merge — never force-push history.

## Agent rules

- Agents work only on spec branches; pushing to `main` or tagging releases is human-only.
- devops maintains the workflows in `.github/workflows/` (spec-driven like everything else); the release workflow itself is a protected path once established.
