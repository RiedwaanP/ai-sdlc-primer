# Adapter: Kiro (IDE + CLI)

Kiro reads `AGENTS.md` from the workspace root automatically (always included, no inclusion modes) — the core works with zero wiring. Kiro's native concepts map closely to this framework, so this adapter is mostly about avoiding duplication.

## Wiring

1. **Instructions**: `AGENTS.md` auto-loads. Don't duplicate content into steering files; add thin steering pointers only where scoping helps (e.g. `.kiro/steering/structure.md`: "Follow standards/engineering-standards.md").
2. **Specs**: Kiro's spec mode natively produces EARS requirements → design → tasks in `.kiro/specs/` — the same shape as our `specs/` templates. Pick ONE home to avoid drift:
   - **Recommended**: keep `specs/` as the source of truth and steer Kiro's spec mode to use our templates and write there, or
   - use `.kiro/specs/` natively and treat it as this repo's `specs/` (update `AGENTS.md` paths accordingly).
3. **Roles**: Kiro CLI custom agents — one agent config per role card, each pinning its tier's model and tool permissions per the card's Access line. In the IDE, paste/reference role cards per session.
4. **Guardrails**: Kiro hooks (`.kiro/hooks/`, JSON v1) support tool-use interception — wire a pre-action hook that checks file paths against `guardrails/protected-paths.txt`, like the Claude Code adapter. Pre-commit + CI remain the backstop.
5. **Model routing**: no BYOK gateway path — Kiro is subscription-based with its own model tiers. Map Plan/Build/Scout to Kiro's available model options in each custom agent config; the routing *policy* (`agents/routing.md`) still applies, only the mechanism differs.
6. **Cost**: no per-request metering via your own keys; track via Kiro's usage/limits plus the `observability/cost-log.md` ledger written by the cost-report prompt.
