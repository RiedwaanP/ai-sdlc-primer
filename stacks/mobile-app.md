# Stack Pack — Mobile App

<!-- POPULATE all <PLACEHOLDERS>; delete unused options. -->

## Stack

- Framework: <React Native+Expo | Flutter | native Swift/Kotlin>
- State: <…> · Local storage: <…> · API client: <generated from contracts/>
- Distribution: <TestFlight/Play internal → stores> · CI: <EAS | fastlane | …>

## Commands

- BUILD_CMD: `<…>` · TEST_CMD: `<…>` · LINT_CMD: `<…>` · TYPECHECK_CMD: `<…>` · DEV_CMD: `<…>`

## Structure

```
src/
  features/<feature>/     # screens + logic + tests co-located
  design/tokens.<ext>     # tokens shared with design source (see design-primer)
  components/             # shared primitives
  services/               # API, storage, push — adapter pattern
  navigation/
e2e/                      # Maestro/Detox — critical journeys only
```

## Naming casing

Files: `kebab-case` (or platform norm) · Components/Types: `PascalCase` · Functions: `camelCase` · Declare final choice: <…>

## Mobile-specific rules

- Offline behavior defined per feature in the spec (Unwanted-pattern REQs for connectivity loss).
- All network calls resilient: timeout, retry policy, user-visible failure state.
- Platform review: permissions minimal + justified in an ADR; store-policy check is part of the review gate for affected features.
- Performance budgets: cold start < <N>s, bundle < <N>MB; measured in CI.

## Design integration

Per `standards/design-primer.md`; tokens must match the design source exactly — mobile drift is the most common design bug.

## Post-deploy verification

- Internal track build installs + smoke journeys pass on <device matrix>; crash-free rate ≥ baseline after staged rollout step 1; rollback = halt rollout + previous binary: `<…>`
