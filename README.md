# Agnostic SDLC Primer — Harness-Neutral, Bring-Your-Own-Key

A clone-and-populate foundation for AI-driven SDLC (spec → plan → tasks → implement → review → deploy) that works with **any agent harness** — Claude Code, GitHub Copilot, Cursor, Codex CLI, Gemini CLI, Aider, Windsurf, Zed — and **any model provider** via your own API keys.

## Design principle

One vendor-neutral core, thin per-harness adapters. The core (specs, standards, constitution, roles, prompts, gates, cost policy) never mentions a vendor. Adapters wire it into each tool's native mechanisms. Enforcement that can't be portable (tool hooks) moves to what IS portable: git pre-commit hooks and CI.

## What's in the box

| Path | Purpose |
|---|---|
| `AGENTS.md` | Core operating manual. The cross-tool standard file — read natively by Copilot, Cursor, Codex, Claude Code, and 25+ other tools. |
| `constitution.md` | Non-negotiable rules (EARS-style), enforced at the review gate + CI. |
| `agents/` | 8 role definitions + capability-tier routing mapped to Anthropic / OpenAI / Google / open-weights. |
| `prompts/` | Lifecycle prompts: spec, plan, tasks, implement, cost-report. Paste, alias, or register per adapter. |
| `guardrails/` | Portable enforcement: protected-paths list, git pre-commit hook, policy doc. |
| `adapters/` | Wiring guides: claude-code, github-copilot, cursor, codex-cli, gemini-cli, byok-gateway. |
| `specs/`, `standards/`, `stacks/`,  `pipeline/` | Same battle order as any spec-driven repo: templates, engineering/testing/security/design standards, stack packs, phase-gated playbook + CI. |
| `observability/` | Provider-agnostic cost policy + telemetry options (gateway metering, cost log). |

## Quick start

1. Copy this folder as your new repo root (it's self-contained — move it anywhere).
2. Fill `<PLACEHOLDERS>` in `AGENTS.md`, `constitution.md`, one `stacks/` pack, and the tier table in `agents/routing.md` (pick your providers).
3. Install the portable guardrails: `cp guardrails/pre-commit .git/hooks/pre-commit && chmod +x .git/hooks/pre-commit`.
4. Wire your harness: follow the matching guide in `adapters/` (5–15 min each; run several side by side if your team is mixed).
5. Optional but recommended for BYOK cost control: stand up a gateway per `adapters/byok-gateway.md` (LiteLLM self-hosted or OpenRouter) — one endpoint, all providers, per-request cost metering.
6. Start work with the spec prompt: `prompts/spec.md`.

## Harness support matrix

| Harness | Reads AGENTS.md | Role agents | Lifecycle prompts | Native hooks |
|---|---|---|---|---|
| Claude Code | ✅ (CLAUDE.md richer) | ✅ subagents | ✅ skills | ✅ |
| GitHub Copilot | ✅ | ✅ custom chat modes | ✅ prompt files | CI only |
| Cursor | ✅ | ◐ rules per glob | ✅ commands | CI only |
| Codex CLI | ✅ (native) | ◐ via prompt | ✅ custom prompts | CI only |
| Gemini CLI | ◐ (GEMINI.md, see adapter) | ◐ via prompt | ✅ custom commands | CI only |
| Anything else | Point it at AGENTS.md | via prompt | paste prompts | CI only |

"CI only" is fine: the pre-commit hook + `pipeline/ci/` enforce protected paths, secret scanning, tests, and spec traceability regardless of which tool wrote the code.

## Cost model

Tiering is by capability class, not vendor: **Plan** (frontier reasoning), **Build** (mid-tier), **Scout** (fast/cheap). `agents/routing.md` maps tiers to whichever providers your keys unlock; `observability/cost-policy.md` sets budgets and escalation. Routed three-tier work typically runs 50–80% cheaper than frontier-everywhere.
