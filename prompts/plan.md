# Prompt: plan — Spec → Implementation Plan

Run on a **Plan-tier** model, **architect** role. Recon via a Scout-tier session if the codebase is large.

---

Adopt `agents/architect.md`. Create the implementation plan for spec {{NNN}}.

1. Verify `specs/{{NNN}}-*/spec.md` has `status: approved`; refuse otherwise.
2. Create `plan.md` from `specs/TEMPLATE-plan.md`: component breakdown, exact interfaces/contracts, data model changes (+ rollback), error handling, test strategy, rollout.
3. Significant decisions (new dependency, pattern deviation, infra change) → ADR in `specs/adr/`, referenced from the plan.
4. State constitution + stack pack compliance explicitly.
5. Every plan element traces to REQ IDs; anything untraceable is scope creep — remove it or flag a spec amendment.
6. Leave `status: draft` and stop for my approval.
