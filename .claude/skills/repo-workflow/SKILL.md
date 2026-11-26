---
name: repo-workflow
description: Use when Swamy asks to run a repository's Claude/GHCP workflow, with or without a stage. Verify startup with start-work before selecting one stage to agree a concept, assess gaps, complete an approved step, verify evidence, or hand off. Prompt maintenance never authorizes execution.
---
<!-- Managed by engineering-governance. Do not edit here; edit in engineering-governance and run scripts/sync-governance.ps1. -->

# Repository workflow

## Select one run

1. A request to create, edit, or review prompts is maintenance, not permission to execute them.
2. Identify the intended repository from the user's request and verify its Git root. In a multi-root workspace, ask if the target is ambiguous. Never infer the target from the skill's installation directory.
3. Before asking for or selecting a stage, run [start-work](../start-work/SKILL.md). Reuse its verified state from this session only if Git and scope are unchanged. If startup is blocked, report the blocker and stop; do not switch branches with dirty files without approval or discard unmerged work.
4. Select exactly one stage: **1 Agree**, **2 Assess**, **3 Complete**, **4 Verify**, or **5 Handoff**. A missing/invalid stage or an unresolved placeholder requires clarification, not a default or a run of every stage.
5. Read the usage section and selected stage only from the target repo's guide: `docs/prompts/01_claude_workflow.md` for Claude Code, or `docs/prompts/02_ghcp_workflow.md` for GitHub Copilot. If the host is unknown, ask which guide to use; if the guide is absent, stop and report the missing path. Do not borrow another repo's guide.
6. Guide prompts supply repo-specific scope; this skill supplies their shared execution contract. When a guide refers back to this skill, continue the current invocation rather than loading it again.

## Shared execution contract

- Follow the repository's `AGENTS.md`, `AGENTS.repo.md`, and relevant scoped rules. Read `CONVENTIONS.md`, relevant `CORRECTIONS.md` entries, and `SESSION_STATE.md` when present. The coordination board is advisory, not a lock.
- Reconcile the README and any relevant active plan or handoff index with Git. Do not load a whole backlog, historical plans, or private memory as a substitute for evidence.
- State the concept, included and excluded files/behaviors, language/stack when relevant, and one observable acceptance check. Reuse explicit agreement; ask only for missing decisions. A backlog, default stack, or illustration is not authorization to implement.
- Work on one selected stage and one agreed edit group. Stop when that stage is complete, a decision blocks it, or after 10 tool operations or 5 minutes, whichever occurs first. Count individual operations inside batches; let an in-flight check finish safely, report its result, and wait for "continue" before starting another block. Do not cancel validation solely to meet the limit.
- Search narrowly, read the relevant full passage or function, and cite `path:line` for findings. Distinguish **observed source**, **executed check**, **user-stated**, and **unverified** evidence. Source inspection is not proof of runtime behavior.
- Preserve settled work unless new evidence affects the approved scope. Raise unresolved choices with the evidence, options, what they block, and the answer needed. Never turn an assumption into a verified fact.
- Do not edit managed copies; change their source in engineering-governance and use its sync workflow only with the affected scope agreed. No commits, pushes, PRs, branch deletion, history rewriting, submodule pointer updates, or deployment without explicit authorization.
- Use only available, authorized tools. An MCP configuration, mentioned tool, or local file is not proof of a running/authenticated service. Do not install or configure MCP servers for this workflow; report missing access and the specific blocked check. Never send private repository material to external services.
- Handle the work directly unless a bounded, context-heavy independent task genuinely warrants delegation. Do not hard-code models or launch parallel agents by default; avoid overlapping edits.
- Learning material is read-only input: follow the shared source-material safeguards, synthesize in your own structure with original examples, and keep public output self-contained. Do not copy another project's domain rules, approval machinery, private paths, or claims of completion.

## Stage 1 - Agree

Read only enough current context to clarify Swamy's concept and the guide's repo-specific questions. Do not create exercises, session folders, product requirements, or code.

Return:

- Concept and intended outcome.
- Included/excluded scope and one small next step.
- Examples and stack, or why a stack is not applicable.
- Acceptance check and any open decision.

Wait for agreement. If an explicit agreement already covers all of these, report it without asking again; do not automatically advance to Stage 2 or 3.

## Stage 2 - Assess

Inspect the named scope without changing authored files. For changed learning input, compare the actual material with maintained notes for coverage and explanatory depth; filenames or earlier passing checks are not evidence of currency.

Return a compact table:

| Finding | Evidence | Impact | Smallest proposed edit | Acceptance check |
| --- | --- | --- | --- | --- |

Include unresolved claims and missing evidence, not speculative defects. Propose one edit group with exact paths and dependencies. Stop for approval; an assessment is not permission to fix its findings.

## Stage 3 - Complete

Require a named, approved step and its acceptance check. Selection of this stage alone does not approve unspecified findings. Reconcile the approval with current files before editing and stop if conflicting concurrent changes appear.

- For code, observe one deterministic test fail for the intended behavior, write the smallest production change, then refactor with relevant tests green. A missing SDK or dependency is not the intended red result.
- For an agreed refactoring of existing behavior, establish the behavioral tests first and keep them green; do not invent a new behavior merely to obtain a red test.
- For documentation, correct only approved gaps and directly dependent links/status. No placeholder implementation, invented answer, or future exercise.
- Verify the actual acceptance check. Record exact commands/results, failures, and skipped checks. Update only directly related documentation with observed progress.
- Each affected README must retain exactly seven distinct relevant badges with seven different medium-tone colors. Where diagrams help, use medium-tone role colors, darker borders, black labels, and an equivalent adjacent fenced `text` fallback.

Stop at the agreed step. A possible next behavior or green commit point is a proposal, not permission to start it or commit.

## Stage 4 - Verify

Make no authored-file edits. Check the selected result against its agreed acceptance criteria, relevant tests or documentation checks, and repo-specific requirements in the guide. Reuse unchanged, observed results from this session; rerun when inputs changed.

Report each criterion as **pass**, **fail**, **blocked**, or **not applicable**, with its evidence. Include content/link consistency, README badge truthfulness/count/colors, and Mermaid/ASCII correspondence when applicable. Lint alone does not prove those properties.

For native skills, distinguish synced-file parity from live discovery and execution. Live verification requires a fresh session in each intended tool, finding the skill, selecting a harmless scoped stage, and observing the expected guide and stop boundary. Never report that check as passed from filenames or sync output alone.

If a criterion fails, propose the smallest repair for approval; do not silently enter Stage 3. Use `reviewer` for large/risky changes under the shared rules, not to duplicate a small direct review.

## Stage 5 - Handoff

Use [handoff](../handoff/SKILL.md) for unfinished work, retaining the guide's repo-specific state. Record the concept, agreed scope, branch/dirty state, exact checks/results, next step, and blockers in the existing active plan or the required plan location. Update an existing handoff index only with a link, not a second task history.

For completed work, give a concise completion summary and the next decision; do not manufacture a plan. Keep durable conventions in repo guidance, not private tool memory. A handoff does not authorize sharing, committing, or another implementation stage.
