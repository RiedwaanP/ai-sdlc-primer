# Cost Policy — Budgets & Discipline (provider-agnostic)

Tier definitions and routing rules live in `agents/routing.md`; this file owns budgets, enforcement, and token discipline.

## Budgets <!-- POPULATE -->

| Scope | Budget | Alert at | Hard action |
|---|---|---|---|
| Per feature (spec→merge) | $<X> | 70% | Pause + cost-report + human go/no-go |
| Per session | $<X> | 70% | Same |
| Per month | $<X> | 80% | Freeze non-critical work |

Enforcement layers:

1. **Advisory** — agents check budgets via `prompts/cost-report.md` at phase ends (Constitution Art. V).
2. **Technical** — hard `max_budget` on gateway keys (`adapters/byok-gateway.md`). Without a gateway, provider-console spend limits per API key are the fallback.

Tip: one gateway virtual key per feature (or per tier) makes cost-per-feature reporting automatic.

## Measurement

See `observability/telemetry.md` for options per setup. Minimum viable: the append-only `cost-log.md`, one line per feature/phase, written by the cost-report prompt.

Minimum dashboard when metered: cost by tier, tokens by role, cost per feature, escalation count. Watch two ratios: Plan-tier share of volume (should be small; if growing, routing is leaking) and cost per merged feature (trend, not absolute).

## Token-efficiency checklist (all agents, all harnesses)

- Load files on demand; grep before read; read sections, not files.
- Sub-sessions/agents return conclusions, not transcripts.
- Keep AGENTS.md + standards lean; deep detail in referenced files loaded on demand.
- Clear/compact context between features; stale context is a silent tax.
- Batch independent tool calls; don't re-read unchanged files.
- Stable instruction files benefit prompt caching on all major providers — don't churn AGENTS.md mid-feature.
