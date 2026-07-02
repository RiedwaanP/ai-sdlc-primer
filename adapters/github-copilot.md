# Adapter: GitHub Copilot (VS Code / coding agent)

Copilot reads `AGENTS.md` natively (repo root). BYOK: Copilot supports bring-your-own-key for Anthropic/OpenAI/Google models in individual plans; org plans use the model picker.

## Wiring

1. **Instructions**: `AGENTS.md` is picked up automatically. Optionally add `.github/copilot-instructions.md` containing one line: "Follow AGENTS.md."
2. **Roles → custom chat modes**: create `.github/chatmodes/<role>.chatmode.md` per role card:
   ```markdown
   ---
   description: Merge-gate reviewer
   model: <pick your Plan-tier model from the model picker/BYOK>
   tools: ['codebase', 'search', 'runCommands']   # match the card's Access line
   ---
   <paste the role card body>
   ```
3. **Prompts → prompt files**: each `prompts/<name>.md` becomes `.github/prompts/<name>.prompt.md` → run as `/<name>` in chat.
4. **Model routing**: no per-subagent auto-routing — switch model per chat mode (step 2) or manually per phase: Plan-tier model for spec/plan/review chats, Build-tier for implementation, small model for recon.
5. **Guardrails**: instructions + pre-commit + CI (`pipeline/ci/`). For the Copilot coding agent (async PRs), branch protection + required CI checks are the hard gate.
6. **Cost**: Copilot is seat-based + premium-request metered; BYOK calls bill your provider account — meter via the gateway (`adapters/byok-gateway.md`) where possible.
