# Stack Pack — Web App / SaaS

<!-- POPULATE all <PLACEHOLDERS>; delete unused options. -->

## Stack

- Frontend: <e.g. React 19 + TypeScript strict + Vite / Next.js>
- API: <e.g. Node+Fastify | Python+FastAPI | Go+chi>
- DB: <e.g. Postgres + migration tool> · Cache: <optional>
- Auth: <e.g. session | OIDC provider>
- Hosting: <e.g. Vercel/Fly/AWS> · IaC: <e.g. Terraform/Pulumi>

## Commands (fills AGENTS.md placeholders)

- BUILD_CMD: `<…>` · TEST_CMD: `<…>` · LINT_CMD: `<…>` · TYPECHECK_CMD: `<…>` · DEV_CMD: `<…>`

## Structure

```
src/
  features/<feature>/      # UI + logic + tests co-located per feature
  design/tokens.<ext>      # design tokens (see standards/design-primer.md)
  components/              # shared, token-consuming components (rule of three)
  server/
    routes/                # thin delivery layer
    domain/                # business logic, no framework imports
    adapters/              # DB, external APIs (repository pattern)
migrations/
e2e/                       # critical journeys only (list below)
```

## Naming casing

Files: `kebab-case` · Types: `PascalCase` · Functions/vars: `camelCase` · Constants: `SCREAMING_SNAKE` · DB: `snake_case` · API JSON: `camelCase`

## Critical E2E journeys <!-- POPULATE -->

1. Sign up → onboard → core action
2. <…>

## API conventions

REST, plural resources, versioned (`/api/v1/`); errors as RFC 9457 problem+json; pagination via cursor; all routes declare authz explicitly.

## Design integration

Per `standards/design-primer.md`. Design MCP: <Figma | Penpot | none — tokens file is truth>.

## Post-deploy verification

- Health endpoint 200; smoke E2E against staging/prod; error-rate and latency within baseline for 15 min; rollback command: `<…>`
