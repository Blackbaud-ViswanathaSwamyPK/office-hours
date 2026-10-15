---
name: handoff
description: Use when a session ends with work unfinished, when context is about to be cleared or compacted, or when the user says "handoff", "wrap up", or "save state". Records Swamy's concept, agreed scope, verified state, exact checks including README badges/diagrams, next step, and blockers for either tool; avoids unnecessary plans for completed work.
---
<!-- Managed by engineering-governance. Do not edit here; edit in engineering-governance and run scripts/sync-governance.ps1. -->

# Handoff

## 1. Collect the facts

- `git status -sb` and `git diff --stat HEAD` (staged and unstaged; plain `git diff --stat` shows unstaged only).
- What you verified this session, and how (commands run and their result).
- Swamy's concept and the agreed next step, including any language/stack or scope decisions. If none was supplied, record "awaiting Swamy's concept"; do not invent follow-up implementation.
- Checks that failed or were not run, and why. Keep verified results separate from expectations.
- Inspect only task-related changes; preserve unrelated dirty work and never include secrets or private session transcripts.

## 2. Write the plan file

Update the plan for this work in `docs/plans/`, or create `docs/plans/<yyyy-mm-dd>-<topic>.md`. Keep the top section current:
If all work is finished, mark an existing plan `State: done`; do not create a new plan just to say nothing remains.

```markdown
## Status (<yyyy-mm-dd>)

- State: in progress
- Branch: <branch>; uncommitted changes: <yes/no>
- Concept and agreed scope: <Swamy's concept and decisions, or awaiting Swamy's concept>
- Done: <item> (verified by <command or check>)
- Validation: <exact command, result, and any failed/skipped checks>
- Next: <the very next step, concrete enough to start without reading this session>
- Blockers and open questions: <or "none">
```

Keep it short. Link to files and line numbers instead of copying code.
Do not call a step done because code was written: record "implemented, not verified" when its acceptance check has not passed.

## 3. Update the durable places

- A milestone finished: update the README progress or status section.
- When updating a README, preserve exactly seven distinct, relevant badges with seven different medium-tone colors. Keep Mermaid diagrams and their adjacent ASCII fallbacks equivalent; record any unverified diagram checks.
- The user taught you a lasting convention: propose the exact line to add to `AGENTS.repo.md` (or to `engineering-governance` if it applies to every repo). Do not add it without agreement.
- The plan is complete: change its status line to `State: done`, so `start-work` skips it.

## 4. Report

Give the plan file path and a three-line summary. Do not commit unless the user asks.
