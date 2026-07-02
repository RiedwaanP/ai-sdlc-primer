# Constitution

Non-negotiable rules. Written as testable EARS statements so any agent can verify compliance. The reviewer agent blocks any merge that violates an article. Amendments require a human-approved ADR.

## Article I — Spec supremacy

- The system SHALL NOT contain code that is not traceable to a requirement in an approved spec.
- WHEN a spec and its implementation conflict, the spec SHALL be treated as correct and either the code fixed or the spec formally amended.

## Article II — Quality gates

- The system SHALL keep `<TEST_CMD>`, `<LINT_CMD>`, and `<TYPECHECK_CMD>` passing on the main branch at all times.
- The system SHALL NOT merge changes that reduce test coverage below <COVERAGE_TARGET>%.
- WHEN a task is completed, its acceptance test SHALL exist and pass before the next task begins.

## Article III — Maintainability

- The system SHALL follow the naming conventions in `standards/engineering-standards.md` with zero exceptions.
- Functions SHALL NOT exceed <MAX_FUNC_LINES=50> lines; files SHALL NOT exceed <MAX_FILE_LINES=400> lines without an ADR.
- The system SHALL NOT introduce a new external dependency without an ADR recording the alternatives considered.
- Public interfaces SHALL have doc comments stating purpose, inputs, outputs, and error behavior.

## Article IV — Security

- The system SHALL NOT store secrets in source, specs, logs, or agent transcripts; secrets live only in the environment or a secret manager.
- The system SHALL validate all external input at the boundary per `standards/security-baseline.md`.
- WHEN a dependency has a known critical CVE, the pipeline SHALL fail.

## Article V — Cost discipline

- Agents SHALL use the lowest routing tier capable of the task (see `observability/cost-policy.md`).
- WHEN a session exceeds its budget alert threshold, the orchestrator SHALL pause and report before continuing.

## Article VI — Human control points

Humans (or a designated approver agent, if delegated by ADR) SHALL approve: specs, plans, ADRs, production deploys, and any change to this constitution, `AGENTS.md`, guardrails, or agent role definitions.

<!-- POPULATE: add project-specific articles below -->
