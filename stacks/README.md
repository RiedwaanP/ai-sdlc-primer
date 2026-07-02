# Stack Packs

A stack pack is the project-type-specific layer: conventions, structure, tooling, deploy path. The core framework (specs, agents, gates, cost policy) never changes per project — only the pack does.

**To use:** pick one pack, fill its `<PLACEHOLDERS>`, and reference it from `AGENTS.md` ("Stack pack:"). Delete the packs you don't use.

**To add a project type** (CLI tool, data pipeline, ML service, game…): copy `api-service.md` as the closest baseline and adapt its sections — keep the same section headings so agents always know where to look.

| Pack | For |
|---|---|
| `web-app.md` | Frontend + API + DB SaaS products |
| `api-service.md` | Headless services, APIs, workers |
| `mobile-app.md` | iOS/Android apps |
