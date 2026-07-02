# Adapter: Codex CLI

AGENTS.md is Codex's native format — zero wiring for instructions. BYOK: `OPENAI_API_KEY`, or any OpenAI-compatible endpoint (your gateway) via provider config in `~/.codex/config.toml`.

## Wiring

1. **Instructions**: `AGENTS.md` at repo root auto-loads (plus `~/.codex/AGENTS.md` globally — keep global empty or minimal to avoid conflicts).
2. **Roles**: no sub-agents — start each phase's session with the right model and role: `codex -m <plan-tier-model>` then "Adopt `agents/architect.md`". 
3. **Prompts → custom prompts**: copy `prompts/*.md` to `~/.codex/prompts/` → invoke as `/spec` etc. (project-local: paste the prompt file).
4. **Model routing**: per-session `-m` flag, or gateway aliases (`plan`/`build`/`scout`) via a custom provider block pointing at LiteLLM/OpenRouter.
5. **Guardrails**: run in the default sandbox (workspace-write); approvals on for commands. Pre-commit + CI are the hard stops.
6. **Cost**: provider billing; gateway for unified metering. Codex `/status` shows session token usage.
