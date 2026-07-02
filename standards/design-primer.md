# Design Primer — UI/UX & Design-to-Code

Applies to stack packs with a UI (web-app, mobile-app). The goal: agents produce consistent UIs from a single design source of truth, not per-screen improvisation.

## Design source of truth

Pick one and record it here: <!-- POPULATE -->

- **Design tool + MCP:** Figma MCP (rich, 15+ tools, heavier token cost) or Penpot MCP (open-source, CSS-native output, ~5 lean tools — cheaper per session). Connect the MCP server in project config so agents query components/tokens directly instead of guessing from screenshots.
- **No design tool?** The design system below IS the source of truth; agents build from tokens + component specs.

MCP access alone gives agents *read* access, not *understanding* — composition rules and conventions must be written down here, or agents will improvise.

## Design tokens (single source, never hardcode)

Define once in `<DESIGN_TOKENS_FILE>` (e.g. `src/design/tokens.{css,ts,json}`):

- Color: semantic names (`--color-surface`, `--color-danger`) — components never reference raw hex.
- Type scale, spacing scale (4/8px grid), radii, shadows, breakpoints, motion durations.
- Dark mode via token remapping, not per-component overrides.

Hook/lint rule: raw hex colors or magic px values in component code fail review.

## Component rules

- Check the component inventory before creating anything new; new components require a note in the plan.
- Components are: token-consuming, variant-driven (props, not forks), accessible by default.
- Composition conventions (layout primitives, page shells): <!-- POPULATE -->

## Accessibility (non-negotiable)

WCAG 2.2 AA: semantic markup, keyboard navigable, visible focus, 4.5:1 contrast, labels on all inputs, reduced-motion respected. Automated a11y checks run in CI; failures block.

## Agent design workflow

1. Architect references design source in the plan (frame/component links or component specs).
2. Implementer queries the design MCP (or tokens file) for exact values — never eyeballs.
3. Screenshot-compare against the design during review for UI tasks (agent takes screenshot, compares, iterates).
4. Deviations from the design system require design-owner sign-off recorded in the task.
