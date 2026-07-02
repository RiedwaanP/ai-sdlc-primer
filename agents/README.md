# Role Cards

Eight harness-neutral roles. Each card is a self-contained system-prompt block: role, tier (see `routing.md`), least-privilege access, rules.

How to use per harness (details in `adapters/`):

- **Sub-agent support** (Claude Code, Copilot chat modes): register each card as an agent/mode with the tier's model and the stated access as its tool permissions.
- **No sub-agents** (Codex CLI, Gemini CLI, plain chat): start the session on the tier's model and paste the role card first, or reference it: "Adopt `agents/reviewer.md`."
- **Access column is a guardrail, not a suggestion**: where the harness can't enforce it (e.g. read-only reviewer), the pre-commit hook + CI in `guardrails/` and `pipeline/ci/` backstop it.
