---
id: NNN
slug: <feature-slug>
status: draft          # draft → approved (human only) → implemented
revision: 1
owner: <human name>
created: YYYY-MM-DD
---

# Spec NNN — <Feature name>

## Outcome

One paragraph: what exists after this ships and why it matters. Measurable where possible.

## Scope

**In scope:** …
**Non-goals (explicit):** …

## Requirements (EARS)

Use EARS patterns; one testable claim each, no "and/or" compounds.

| ID | Pattern | Requirement |
|---|---|---|
| REQ-001 | Ubiquitous | The system SHALL … |
| REQ-002 | Event | WHEN <trigger>, the system SHALL … |
| REQ-003 | State | WHILE <state>, the system SHALL … |
| REQ-004 | Unwanted | IF <error condition>, THEN the system SHALL … |
| REQ-005 | Optional | WHERE <feature enabled>, the system SHALL … |

## Constraints

Performance, compatibility, compliance, budget (cost ceiling for this feature per `observability/cost-policy.md`).

## Prior decisions

Relevant ADR links; existing patterns this must follow.

## Edge cases & error behavior

Enumerate; each becomes a REQ or is explicitly out of scope.

## Verification criteria

How we know it's done: named acceptance tests per REQ, plus any manual checks.

## Open questions

Unresolved items blocking approval. Must be empty when status → approved.
