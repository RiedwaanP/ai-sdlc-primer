# Prompt: tasks — Plan → Task List

Run on a **Plan-tier** model, **architect** role.

---

Adopt `agents/architect.md`. Break plan {{NNN}} into tasks.

1. Verify `plan.md` is approved; refuse otherwise.
2. Create `tasks.md` from `specs/TEMPLATE-tasks.md`. Each task:
   - **Atomic**: one focused session, ~1–2 files; split anything larger.
   - **Ordered**: dependencies explicit; independent tasks marked `[P]`.
   - **Traceable**: lists the REQ IDs it satisfies.
   - **Verifiable**: names its acceptance test + the command proving it done.
   - **Tiered**: tagged `build` (default) | `scout` (docs/lookups) | `plan` (justify).
3. First tasks: test scaffolding/setup. Last tasks: docs, review-gate prep.
4. Estimate cost vs the feature budget in `observability/cost-policy.md`; flag overruns.
5. Leave `status: draft` and stop for my approval.
