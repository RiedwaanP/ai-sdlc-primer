# Engineering Standards

The goal: any agent or human, given only the spec and these standards, can safely understand and extend the code. Consistency is enforced by the reviewer gate; these rules are not stylistic preferences.

## Naming (zero-exception rules)

- One concept, one name, everywhere. Pick `user` or `account` — never both for the same thing. Maintain the glossary below.
- Names state intent, not mechanics: `retryFailedPayments()` not `processLoop2()`.
- Casing per stack pack conventions (declared there once, followed everywhere): files, types, functions, constants, DB columns, API fields.
- Booleans read as predicates: `isExpired`, `hasAccess`, `canRetry`.
- No abbreviations except the glossary's approved list. No single-letter names outside trivial lambdas/indexes.
- Test names encode traceability: include the requirement ID (`REQ-004_rejects_expired_token`).

### Glossary <!-- POPULATE as the domain vocabulary emerges -->

| Term | Meaning | Never call it |
|---|---|---|

## Structure

- Feature-oriented foldering per the stack pack; shared code earns its place only after a third consumer exists (rule of three).
- Dependency direction is one-way: domain logic never imports from delivery layers (HTTP/UI/CLI).
- Functions ≤ 50 lines, files ≤ 400 lines (Constitution Art. III); split by responsibility, not line-count gaming.
- No circular imports; the linter enforces it.

## Patterns

- Composition over inheritance; inheritance depth > 2 requires an ADR.
- Dependency injection for anything with I/O (DB, HTTP, clock, random) — this is what makes code testable by agents.
- Errors: fail fast at boundaries, typed/structured errors inside; never swallow exceptions; never return sentinel values where an error type exists.
- Immutability by default; mutation is a deliberate, local choice.
- No global mutable state. Configuration enters at the composition root.
- Repository/adapter pattern at every external system boundary (DB, third-party APIs) so implementations are swappable and mockable.

## Comments & docs

- Doc comments on all public interfaces: purpose, inputs, outputs, errors.
- Inline comments explain *why*, never *what*. Code that needs a *what* comment gets rewritten.
- No commented-out code, no `TODO` without a linked task ID.

## Agent-maintainability additions

- Every module's entry file starts with a 2–4 line header comment: what this module owns and what it must never do. Cheap context for future agents.
- Prefer explicit over clever: no metaprogramming, reflection, or magic strings where a plain function works.
- Keep diffs reviewable: one task = one coherent diff. Never mix refactoring with behavior change.
