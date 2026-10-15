---
applyTo: "**/*.ts,**/*.tsx,**/tsconfig*.json,**/package.json"
---
<!-- Managed by engineering-governance. Do not edit here; edit in engineering-governance and run scripts/sync-governance.ps1. -->

# TypeScript guidance (starter, expand when this track begins)

- Use `strict: true`. No `any`; prefer `unknown` and narrow.
- Test runner: Vitest. Name tests with `describe('<unit>')` and `it('<behavior>')`.
- Follow the TDD loop in `AGENTS.md`: failing test first, then the simplest code.
- Use Prettier and ESLint with the repo config. Keep modules small and pure where possible.
- Inject time, randomness, and I/O so tests stay deterministic.
- These are defaults for new projects. Preserve existing frameworks and tooling; use the repo's configured commands and validate the smallest relevant scope.
