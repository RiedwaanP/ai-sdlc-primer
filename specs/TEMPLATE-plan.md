---
spec: NNN
status: draft          # draft → approved (human only)
created: YYYY-MM-DD
---

# Plan NNN — <Feature name>

## Approach summary

One paragraph. Cite the requirement IDs this plan covers (must be all of them).

## Component breakdown

| Component | Responsibility | Files (exact paths) | Requirements |
|---|---|---|---|
| … | … | `src/…` | REQ-001, REQ-002 |

## Interfaces & contracts

Exact signatures/schemas the implementer must produce — function signatures, API routes with request/response shapes, events. No hand-waving; Build-tier agents implement this verbatim.

## Data model changes

Migrations, new entities, indexes. Include rollback.

## Error handling

Failure modes per component and the required behavior (maps to Unwanted-pattern REQs).

## Test strategy

Test types per component; fixtures needed; what's mocked vs real.

## ADRs

| ADR | Decision |
|---|---|
| adr/NNN-… | … |

## Rollout

Feature flags, migration order, deploy sequence, rollback trigger.

## Constitution compliance

Explicit check against each article. Note any tension and its resolution.
