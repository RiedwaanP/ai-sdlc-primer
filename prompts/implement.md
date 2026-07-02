# Prompt: implement — Tasks → Reviewed Code

Run on a **Build-tier** model (implementer/test-engineer roles). Switch to Plan-tier for step 5's review gate — different session/model if your harness has no sub-agents.

---

Execute the approved `specs/{{NNN}}-*/tasks.md`, one task at a time.

1. Verify `tasks.md` is approved. Load only the next incomplete task.
2. Adopt the role matching the task tier: `build` → `agents/implementer.md` (tests → `agents/test-engineer.md`), `scout` → `agents/scout.md`/`agents/doc-writer.md`. Run `[P]` tasks in parallel only if the harness supports sub-agents.
3. Per task: acceptance test passes, lint/typecheck clean, checkbox ticked. A failing task is never marked done.
4. Escalation: two failed attempts → escalate one tier (see `agents/routing.md`), log `escalated: <reason>` in tasks.md. Three failures at Plan tier → stop and ask me.
5. All tasks done → review gate on the full diff: run `agents/reviewer.md` then `agents/security-auditor.md` on a Plan-tier model. BLOCK findings become new tasks; loop until both APPROVE. Record verdicts in tasks.md.
6. Finish with a report: REQs satisfied, tests added, escalations, session cost (`prompts/cost-report.md`).

Guardrails: never edit protected paths (`guardrails/protected-paths.txt`); never skip the review gate; never batch tasks into one giant diff.
