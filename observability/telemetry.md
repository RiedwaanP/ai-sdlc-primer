# Telemetry Options (pick what matches your setup)

| Setup | Mechanism | Effort | What you get |
|---|---|---|---|
| BYOK gateway (recommended) | LiteLLM spend tracking / OpenRouter activity | Low | Every request, every harness, every provider: cost, tokens, latency, per-key budgets |
| Claude Code direct | Built-in OTel (`CLAUDE_CODE_ENABLE_TELEMETRY=1` + OTLP exporter → Grafana/SigNoz/Datadog/Langfuse) | Medium | Rich harness-level metrics, traces, per-session cost |
| Other harnesses direct | Provider consoles (Anthropic/OpenAI/Google usage pages) per key | None | Coarse spend per key; no per-feature split |
| No infrastructure | `cost-log.md` written by `prompts/cost-report.md` | None | Honest ledger, human-granularity |

Recommendation: gateway metering as the baseline (works for every harness identically), plus harness-native telemetry where it's free to turn on. Tag or key requests per feature (gateway virtual keys or OTel resource attributes) so cost-per-feature is queryable — that's the number that makes the routing policy accountable.
