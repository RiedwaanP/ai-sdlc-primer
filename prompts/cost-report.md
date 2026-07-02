# Prompt: cost-report — Session Cost Summary

Run on any tier (Scout is fine).

---

Summarize this session's model spend.

1. Pull usage from whichever source exists: harness cost command (e.g. Claude Code `/cost`), gateway dashboard/API (LiteLLM `/spend`, OpenRouter activity), or provider console export. See `observability/telemetry.md`.
2. Report: total cost, tokens by tier (Plan/Build/Scout), cost per lifecycle phase if distinguishable.
3. Compare against `observability/cost-policy.md` thresholds: under alert → note headroom; over → pause and wait for my go-ahead (Constitution Art. V).
4. Flag routing waste: Plan-tier usage on search/read/doc work is a routing violation — name the offending step.
5. Append one line to `observability/cost-log.md`: `date | feature | phase | cost | notes`.
