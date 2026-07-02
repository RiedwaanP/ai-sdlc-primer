# Adapter: Cursor

Cursor reads `AGENTS.md` natively. BYOK: Settings → Models → API Keys (OpenAI/Anthropic/Google/OpenRouter-compatible base URL).

## Wiring

1. **Instructions**: `AGENTS.md` auto-loads. Use `.cursor/rules/*.mdc` only for glob-scoped rules (e.g. attach `standards/design-primer.md` guidance to `src/features/**` UI files):
   ```markdown
   ---
   description: Design rules for UI code
   globs: ["src/features/**", "src/components/**"]
   ---
   Follow standards/design-primer.md: tokens only, no raw hex/px.
   ```
2. **Roles**: no persistent sub-agents — reference cards in chat: "Adopt `agents/implementer.md`." Pin the tier's model in the model dropdown per session.
3. **Prompts → commands**: put `prompts/*.md` in `.cursor/commands/` → invoke as `/spec` etc.
4. **Model routing**: manual per session/phase, or point the custom base URL at your BYOK gateway and expose `plan`/`build`/`scout` aliases as selectable models.
5. **Guardrails**: pre-commit + CI are the hard stops (Cursor has no pre-action hooks). Keep auto-run/YOLO mode off, or allowlist commands narrowly.
6. **Cost**: with BYOK keys usage bills your provider accounts; the gateway gives unified metering.
