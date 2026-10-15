---
paths:
  - "**/*.py"
  - "**/pyproject.toml"
---
<!-- Managed by engineering-governance. Do not edit here; edit in engineering-governance and run scripts/sync-governance.ps1. -->

# Python guidance (starter, expand when this track begins)

- For new projects, Python 3.12+ with type hints and strict `mypy` or `pyright`. Preserve existing supported runtimes and tooling unless a migration is requested.
- Test runner: pytest. Name tests `test_<behavior>`; use `@pytest.mark.parametrize` for tables.
- Follow the TDD loop in `AGENTS.md`: failing test first, then the simplest code.
- Lint and format with Ruff. Manage dependencies in `pyproject.toml`.
- Inject time, randomness, and I/O so tests stay deterministic.
- These are defaults for new projects. For existing code, use the repo's configured test, lint, and format commands; validate the smallest relevant scope.
