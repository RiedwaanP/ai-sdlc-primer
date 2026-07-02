# Adapter: Gemini CLI

Gemini CLI's native context file is `GEMINI.md`. BYOK: `GEMINI_API_KEY` (or Vertex AI credentials).

## Wiring

1. **Instructions**: either set `"contextFileName": "AGENTS.md"` in `.gemini/settings.json`, or create `GEMINI.md` containing: "Read and follow AGENTS.md." (Don't duplicate content — one source of truth.)
2. **Roles**: no sub-agents — "Adopt `agents/<role>.md`" per session; set the tier's model with `-m` (Pro for Plan, Flash for Build, Flash-Lite for Scout).
3. **Prompts → custom commands**: create `.gemini/commands/<name>.toml` per lifecycle prompt:
   ```toml
   description = "Idea → EARS spec"
   prompt = "Follow the workflow in prompts/spec.md for: {{args}}"
   ```
4. **Model routing**: per-session `-m`, or point at the gateway if you proxy Gemini through it.
5. **Guardrails**: sandbox mode on; pre-commit + CI are the hard stops.
6. **Cost**: Google AI Studio/Vertex billing; gateway for unified metering.
