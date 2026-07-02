# Stack Pack — API / Backend Service

<!-- POPULATE all <PLACEHOLDERS>; delete unused options. -->

## Stack

- Language/framework: <e.g. Go+chi | Python+FastAPI | Node+Fastify | Rust+axum>
- DB: <…> · Queue/events: <optional> · Cache: <optional>
- Hosting: <containers on …> · IaC: <…>

## Commands

- BUILD_CMD: `<…>` · TEST_CMD: `<…>` · LINT_CMD: `<…>` · TYPECHECK_CMD: `<…>` · DEV_CMD: `<…>`

## Structure

```
src/ (or cmd|internal per language norms)
  domain/          # entities + business rules, zero framework imports
  usecases/        # application services, orchestrate domain + ports
  adapters/        # DB repos, external API clients, queue consumers
  delivery/        # HTTP/gRPC handlers — thin, validation + mapping only
migrations/
contracts/         # OpenAPI/proto — the API contract is spec-adjacent, versioned
```

Dependency rule: delivery → usecases → domain. Adapters implement ports defined by usecases. Never reversed.

## Naming casing <!-- adjust per language norms -->

Per language standard (`gofmt`/PEP8/etc.) — declare here once: <…>

## API conventions

- Contract-first: OpenAPI/proto in `contracts/` updated in the same task as the code; CI diff-checks contract vs implementation.
- Versioning: <URL | header>; breaking changes require new version + deprecation window.
- Errors: structured (RFC 9457 or gRPC status + details); idempotency keys on mutating endpoints where retries occur.
- Observability: structured logs w/ request ID, RED metrics per endpoint, traces propagated.

## Post-deploy verification

- Health/readiness green; contract smoke tests against the live env; consumer-facing SLO dashboards within baseline; rollback: `<…>`
