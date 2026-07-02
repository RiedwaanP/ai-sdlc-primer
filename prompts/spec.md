# Prompt: spec — Idea → Specification

Run on a **Plan-tier** model, **architect** role (`agents/architect.md`).

---

Adopt `agents/architect.md`. Create a specification for: {{IDEA}}

1. Create `specs/NNN-<slug>/spec.md` from `specs/TEMPLATE-spec.md` (NNN = next number).
2. Ask me clarifying questions for anything ambiguous — audience, scope boundaries, non-goals, constraints, data, edge cases — before writing requirements. Never invent requirements.
3. Write requirements as EARS statements with IDs (`REQ-001`…), each testable in isolation.
4. Include: outcomes, scope + explicit non-goals, constraints, prior decisions (link ADRs), edge cases, verification criteria, open questions.
5. Leave `status: draft`; list remaining open questions and stop. I will set `status: approved`.

Do not proceed to planning until approved.
