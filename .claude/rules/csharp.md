---
paths:
  - "**/*.cs"
  - "**/*.csproj"
  - "**/*.slnx"
  - "**/*.sln"
  - "**/Directory.*.props"
---
<!-- Managed by engineering-governance. Do not edit here; edit in engineering-governance and run scripts/sync-governance.ps1. -->

# C# guidance

## Platform and style

- For new projects, target .NET 10 LTS (`net10.0`). Preserve existing target frameworks and tooling unless an upgrade is requested.
- Enable `<Nullable>enable</Nullable>`, `<ImplicitUsings>enable</ImplicitUsings>`, and `<TreatWarningsAsErrors>true</TreatWarningsAsErrors>` via `Directory.Build.props` in new projects; follow existing repo configuration when maintaining code.
- Manage package versions centrally in `Directory.Packages.props`.
- Use file-scoped namespaces, `record` for immutable data, and `sealed` classes by default.
- Prefer constructor injection and small interfaces defined where they are consumed.
- Use `async`/`await` end to end. Name async methods with the `Async` suffix and accept a `CancellationToken` on I/O methods.

## Testing

- Default for new projects: xUnit v3 (`xunit.v3`). Use the repo's configured test runner for existing projects and run the smallest relevant test selection.
- Projects: `Foo` (production) and `Foo.Tests` (tests), side by side.
- Test class per unit: `FooTests`. Test method: `Method_Scenario_ExpectedResult`.
- Use `[Fact]` for single cases and `[Theory]` with `[InlineData]` / `[MemberData]` for tables.
- Assertions: xUnit `Assert` by default. Add Shouldly only if the readability gain is clear.
- Test doubles: NSubstitute, only at boundaries. Prefer hand-written fakes for simple collaborators.
- Inject `TimeProvider` instead of calling `DateTime.UtcNow`.
- Coverage via Coverlet is informational. Do not chase a number at the cost of meaningful tests.
