# Adapter: Claude Code

Claude Code reads `AGENTS.md`; a `CLAUDE.md` symlink/copy also works. Richest wiring of any harness.

## Wiring

1. **Roles → subagents**: for each `agents/*.md` card, create `.claude/agents/<role>.md` with frontmatter mapping tier → model alias and access → tools:
   ```markdown
   ---
   name: reviewer
   description: Merge-gate review. MUST run on every completed feature diff.
   model: opus            # Plan=opus · Build=sonnet · Scout=haiku
   tools: Read, Grep, Glob, Bash   # match the card's Access line; read-only roles get no Edit/Write
   ---
   <paste the role card body>
   ```
2. **Prompts → skills**: each `prompts/<name>.md` becomes `.claude/skills/<name>/SKILL.md` (add name/description frontmatter) → invocable as `/spec`, `/plan`, etc.
3. **Guardrails → hooks** (hardening beyond pre-commit/CI): PreToolUse hook on Edit|Write that greps the file path against `guardrails/protected-paths.txt`, exit 2 to block. Register in `.claude/settings.json`.
4. **Cost**: `/cost` built-in; for dashboards set `CLAUDE_CODE_ENABLE_TELEMETRY=1` + OTLP exporter env vars, or route through the BYOK gateway (`ANTHROPIC_BASE_URL` → LiteLLM) for unified cross-provider metering.

## Notes

- BYOK: `ANTHROPIC_API_KEY` directly, or gateway base URL for tier aliases + metering.
- If you maintain the Claude-native primer (this repo's sibling), just use that — it's this adapter fully expanded.
