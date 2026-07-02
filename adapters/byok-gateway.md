# Adapter: BYOK Gateway (recommended backbone)

One OpenAI-compatible endpoint in front of all your provider keys. Solves the two things harnesses can't do uniformly: **tier aliasing** (swap providers without touching any config) and **unified cost metering** (every request, every harness, one dashboard).

## Option A — LiteLLM (self-hosted, open source)

```yaml
# litellm-config.yaml — tier aliases; POPULATE with your chosen models per agents/routing.md
model_list:
  - model_name: plan
    litellm_params: { model: anthropic/claude-opus-latest, api_key: os.environ/ANTHROPIC_API_KEY }
  - model_name: build
    litellm_params: { model: anthropic/claude-sonnet-latest, api_key: os.environ/ANTHROPIC_API_KEY }
  - model_name: scout
    litellm_params: { model: gemini/gemini-flash-lite-latest, api_key: os.environ/GEMINI_API_KEY }
  # Mix providers freely per tier; add fallbacks:
router_settings:
  fallbacks: [{ plan: [build] }]   # never fall back UP a tier for cost reasons; down only by design
general_settings:
  master_key: os.environ/LITELLM_MASTER_KEY
```

Run: `litellm --config litellm-config.yaml` → endpoint `http://localhost:4000`. Cost tracking is built in: per-key/per-model spend via `/spend` endpoints and the admin UI; set budgets + alerts per virtual key (one key per project or per tier = cost-per-feature reporting).

## Option B — OpenRouter (managed)

One API key, 400+ models, BYOK mode routes calls through your own provider keys (1M BYOK requests/month free, then ~5% routing fee). Activity dashboard gives per-request cost. Less control, zero ops.

## Pointing harnesses at the gateway

- Claude Code: `ANTHROPIC_BASE_URL=<gateway>` (LiteLLM proxies Anthropic-format)
- Codex CLI / Cursor / others: custom OpenAI-compatible provider → `<gateway>/v1`, model names `plan|build|scout`
- Anything speaking OpenAI API: works as-is.

## Budget enforcement

Set hard budgets on gateway keys (LiteLLM: `max_budget` per key; OpenRouter: key limits). This is the only *technical* budget stop in the framework — harness-level budgets are advisory. Wire alert → the pause behavior in `observability/cost-policy.md`.
