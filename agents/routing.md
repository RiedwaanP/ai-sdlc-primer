# Capability-Tier Routing (BYOK)

Tiers are capability classes, not vendors. Map each tier to the provider(s) your keys unlock — fill the table, delete unused columns. Aliases > pinned model IDs; re-check the mapping quarterly, model lineups move fast.

## Tier map <!-- POPULATE: keep one or more columns -->

| Tier | Purpose | Anthropic | OpenAI | Google | Open-weights (self-host/Together etc.) |
|---|---|---|---|---|---|
| **Plan** | Specs, architecture, review gate, hard debugging | `opus` (or Fable-class) | frontier reasoning tier (GPT-5.x / o-series) | Gemini Pro (thinking) | largest available (e.g. DeepSeek-R/Llama-largest) |
| **Build** | Implementation, tests, refactors, CI/CD | `sonnet` | mid coding tier | Gemini Flash (larger) | mid coder (e.g. Qwen-Coder-mid) |
| **Scout** | Search, reads, summaries, docs | `haiku` | mini/nano tier | Gemini Flash-Lite | small fast model |

Relative cost is roughly 15–25× (Plan) : 3–5× (Build) : 1× (Scout). Healthy routing puts 60–70% of volume on Build tier.

## How routing is applied per harness

- **Harness with per-agent models** (Claude Code subagents, Copilot chat modes): set the tier's model in each role's config — see `adapters/`.
- **Harness with one session model**: run phases in separate sessions — Plan-tier session for spec/plan/review, Build-tier for implementation, Scout-tier for recon.
- **Gateway routing** (recommended for BYOK): point every harness at one LiteLLM/OpenRouter endpoint and define tier aliases there (`plan`, `build`, `scout` → concrete models). One place to swap providers, one place to meter cost. See `adapters/byok-gateway.md`.

## Rules (same as cost policy — this table is referenced by all role cards)

1. Default down: unsure → try the cheaper tier first.
2. Reconnaissance is ALWAYS Scout-tier.
3. Escalate on evidence: 2 failed attempts → one tier up, logged in `tasks.md`.
4. Review gate is always Plan-tier; never economize there.
5. Budgets + breach behavior: `observability/cost-policy.md`.
