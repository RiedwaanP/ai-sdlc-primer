# Testing Standards

## Principles

- Tests are the executable half of the spec: every REQ maps to ≥1 test named with its ID.
- Test behavior via public interfaces; refactors that preserve behavior must not break tests.
- A failing test is information, never an obstacle — weakening/skipping/deleting to go green is a constitution violation.

## Pyramid & budgets

| Layer | Target share | Scope | Speed budget |
|---|---|---|---|
| Unit | ~70% | Pure logic, single module, injected fakes | ms each |
| Integration | ~25% | Module + real adapter (DB in container, etc.) | <5s each |
| E2E | ~5% | Critical user journeys only (list them in the stack pack) | minutes total |

Coverage floor: <COVERAGE_TARGET>% lines, enforced in CI. Coverage is a floor, not a goal — assertions must be meaningful.

## Rules

- Arrange-Act-Assert, one behavior per test.
- Deterministic: no real time, network, or randomness — inject clock/RNG (see DI rule in engineering-standards).
- Fixtures are factories with sensible defaults + explicit overrides; no giant shared fixture files.
- Every bug fix ships with a regression test that failed before the fix.
- Flaky test = P1 task; quarantine (explicitly marked, with task ID) is the only alternative to fixing.

## Agent workflow

- test-engineer writes acceptance tests from the task's REQ IDs *before or alongside* implementation.
- The implementer never edits tests to make them pass; test changes route back to test-engineer with justification.
