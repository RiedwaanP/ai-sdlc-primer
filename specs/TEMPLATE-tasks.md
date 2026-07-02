---
spec: NNN
status: draft          # draft → approved (human only)
estimated_cost: $X.XX  # against feature budget in observability/cost-policy.md
---

# Tasks NNN — <Feature name>

Legend: `[P]` = parallelizable · tier: build | scout | plan · Every task lists REQs + its acceptance check.

## Phase 1 — Setup & test scaffolding

- [ ] T-001 (build) Set up test fixtures for <feature> — REQ-all — check: `<TEST_CMD> --filter NNN` runs green (empty)

## Phase 2 — Implementation

- [ ] T-002 (build) Implement <component> in `src/<path>` — REQ-001, REQ-002 — check: test `REQ-001*` passes
- [ ] T-003 (build) [P] Implement <component> in `src/<path>` — REQ-003 — check: test `REQ-003*` passes

## Phase 3 — Integration & hardening

- [ ] T-00N (build) Wire components; error paths per plan §Error handling — REQ-004 — check: test `REQ-004*` passes
- [ ] T-00N (build) Full suite + lint + typecheck green — check: `<TEST_CMD> && <LINT_CMD> && <TYPECHECK_CMD>`

## Phase 4 — Docs & gate

- [ ] T-00N (scout) Update docs/CHANGELOG (doc-writer) — check: docs match shipped behavior
- [ ] T-00N (plan) Review gate: reviewer + security-auditor APPROVE — check: verdicts recorded below

## Escalations log

| Task | From→To tier | Reason |
|---|---|---|

## Review verdicts

- reviewer: —
- security-auditor: —
