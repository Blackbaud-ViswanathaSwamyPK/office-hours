# Folder structure

Office-hours material belongs to the session where it is used. Repository
guides and tooling live outside the session folders.

## Layout

```text
office-hours/
|-- README.md                    Start here: purpose, workflow, and progress
|-- LICENSE                      Terms for reuse
|-- AGENTS.md, AGENTS.repo.md    Shared standards and office-hours rules
|-- CLAUDE.md                    Entry point for Claude Code
|-- CONVENTIONS.md               How to prepare and check session material
|-- SESSION_STATE.md             Coordination for concurrent repository edits
|-- HANDOFF.md, MEMORY.md        Indexes of unfinished work and durable knowledge
|-- CORRECTIONS.md               Verified mistakes and their corrections
|-- .gitignore, .gitattributes   Git exclusions and file attributes
|-- .markdownlint*.{json,jsonc}  Markdown check configuration
|-- .claude/                     Rules, agents, and skills
|-- .github/                     Copilot instructions, agents, and lint workflow
|-- docs/
|   |-- 01-folder-structure.md   This guide
|   `-- prompts/                 Claude and Copilot repository workflow guides
`-- sessions/
    `-- 2026-11-27-understanding-llms/
        `-- notes.md             Theory, discussion prompts, Q&A, and follow-ups
```

## What belongs where

| Path | Holds | Keep out | Status |
| --- | --- | --- | --- |
| Repository root | Overview, license, rules, and coordination files | A talk's agenda or Q&A | Present |
| `.claude/`, `.github/` | Assistant tooling and repository automation | Session examples | Present |
| `docs/` | Guides for people maintaining this repository | Audience notes and runnable demos | Present |
| `docs/prompts/` | Prompts for working on the repository | Prompts used to demonstrate a model during a talk | Present |
| `sessions/<yyyy-mm-dd>-<topic>/` | One session's Markdown, starting with `notes.md` | Other sessions, slide decks, or customer data | Present |
| A session's `src/` | Code used to run that session's demos | Markdown-only demos or empty starter folders | Optional; not created |

## Inside a session: Understanding LLMs

The [Understanding LLMs notes](../sessions/2026-11-27-understanding-llms/notes.md)
hold the agenda and discussion questions. No `src/` is needed for a theory
session. Add that folder only when a session has runnable code.

## Keeping the guide current

Use [CONVENTIONS.md](../CONVENTIONS.md) when preparing a session. When the
layout changes, update the tree, the status table, and the progress in the
[README](../README.md). Mark `src/` present only when it contains demo code.
