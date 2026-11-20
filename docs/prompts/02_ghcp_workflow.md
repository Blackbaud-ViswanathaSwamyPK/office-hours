# GHCP prompts for office-hours

## Usage

Use these in GitHub Copilot with this repository selected. In a multi-root VS Code workspace, identify the target repo explicitly; an active editor or attachment does not select the work.

Choose one prompt, replace its angle-bracket fields, and paste that block only. Reading or maintaining this guide does not execute it. Every prompt uses the [shared workflow contract](../../.claude/skills/repo-workflow/SKILL.md); load it explicitly if native discovery is unavailable.

Native entry: `/repo-workflow` followed by the stage number and the same scope fields, where exposed by the installed surface. Verify it in a fresh session's skill/customization list. The skill reads this guide's selected stage; never run all five. See the [Claude equivalent](01_claude_workflow.md).

## 1. Agree the concept

```text
Use repo-workflow stage 1 in office-hours.
Concept: <session topic or question>.
Agree audience needs without identities, scope, expected outcome, session
date/slug if creating material, and whether notes, slides, or a demo are needed.
Agree a stack and testable behavior only for an explicitly requested demo.
Do not create a session folder or invent questions/answers before agreement.
```

## 2. Assess gaps

```text
Use repo-workflow stage 2 in office-hours.
Scope: <agreed topic or existing session notes/material>.
Check agenda, questions, evidence-backed answers, and unresolved follow-ups.
Separate verified answers from assumptions; inspect demo behavior and tests
only when a demo exists. Identify private data that must not reach public notes
without repeating it in findings. Use anonymized questions and original examples.
Propose one bounded material update; do not expand it into a course or exercise.
```

## 3. Complete the approved step

```text
Use repo-workflow stage 3 in office-hours.
Approved step: <session date/slug, material, and exact scope>.
Acceptance: <observable learning outcome or demo behavior>.
Keep agenda, questions, answers, and follow-ups in
sessions/<yyyy-mm-dd>-<topic>/notes.md. Add slides/ or demos/ only if agreed.
Keep unanswered questions explicit, cite checked facts, and omit personal data,
credentials, and customer information. Do not manufacture attendance or answers.
For a demo, use one intended failing test and the minimum passing behavior.
Propose exercise-sized follow-ups for another repo; do not implement them here.
```

## 4. Verify the result

```text
Use repo-workflow stage 4 in office-hours.
Scope: <approved session material or demo>.
Acceptance: <agreed outcome>.
Check that each scoped question has an evidence-backed answer or an explicit
open follow-up. Check links, original illustrations, and absence of private data.
Run npx --yes markdownlint-cli2@0.23.3 with Node.js 22+.
Run actual demo tests/build only if tooling exists and the demo changed.
Check seven distinct badges/colors per affected README and useful diagram
pairs. Prepared material does not prove that a session occurred or a demo ran.
Do not publish, schedule, or create a follow-up session.
```

## 5. Hand off

```text
Use repo-workflow stage 5 in office-hours.
Scope: <completed or unfinished session preparation>.
Retain topic, date/slug if agreed, material paths, verified answers, open
questions, exact checks, next preparation step, and blockers.
Keep Q&A in session notes; link to it rather than copying it into a work plan.
Do not include attendee identities or turn a follow-up into unapproved work
in another repository. Keep the existing handoff index link-only.
```
