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
`-- sessions/                    Planned; no session folders exist yet
    `-- <yyyy-mm-dd>-<topic>/    One folder per session, dated once
        |-- notes.md             Agenda, demo prompts, Q&A, and follow-ups
        `-- src/                 Optional; runnable demo code only
```

## What belongs where

| Path | Holds | Keep out | Status |
| --- | --- | --- | --- |
| Repository root | Overview, license, rules, and coordination files | A talk's agenda or Q&A | Present |
| `.claude/`, `.github/` | Assistant tooling and repository automation | Session examples | Present |
| `docs/` | Guides for people maintaining this repository | Audience notes and runnable demos | Present |
| `docs/prompts/` | Prompts for working on the repository | Prompts used to demonstrate a model during a talk | Present |
| `sessions/<yyyy-mm-dd>-<topic>/` | One session's Markdown, starting with `notes.md` | Other sessions, slide decks, or customer data | Planned |
| A session's `src/` | Code used to run that session's demos | Markdown-only demos or empty starter folders | Optional; not created |

## Inside a session: Understanding LLMs

Use one folder per session, named with the session date and topic. For this
talk, use `sessions/<yyyy-mm-dd>-understanding-llms/` once the date and scope
are confirmed. Keep the agenda, demo prompts, fictional timetable, anonymized
Q&A, and follow-ups in `notes.md`. All three demos below can run from those
notes; no slides or source files are needed.

Add `src/` inside the session folder only for runnable demo code. For example,
if a tokenizer is implemented later, put its code in `src/01_tokenization/`
and link to it from the first demo in `notes.md`. Do not repeat the date under
`src/` or create empty placeholder folders.

### Example: what goes in the notes

The proposed 30-minute session uses the following three demos and a closing
discussion. Each demo needs only Markdown instructions, not its own folder.

1. **See the tokens (5 minutes).** Enter `The night train leaves at 8:45.` in
   a tokenizer. Ask the audience to guess the token boundaries before revealing
   them. Replace `8:45` with `eight forty-five` and compare the two displays:
   the departure time is the same, but the input tokens are different.
2. **Predict what comes next (8 minutes).** Ask for completions of
   `At the station, the conductor raised her ___`. Then put
   `The platform was too noisy for anyone to hear her.` before it and vote
   again. Use the changed guesses to illustrate how context affects the next
   token. A model selects a token, adds it to the context, and repeats; the
   audience vote illustrates the idea, not the model's actual probabilities.
3. **Check an answer against evidence (7 minutes).** Give the model a fictional
   timetable entry: `Night train | 8:45 | Platform 3`. Ask which platform to
   use and what the fare is. Have the audience point to the evidence for each
   answer: the entry gives a platform but no fare. Add `Fare: $12` and ask
   again. The comparison works whether the model guessed or declined to guess.

**Q&A and closing check (10 minutes):** Change the fare to `$15`. Ask someone
to explain why the model can now give a different answer without retraining:
the prompt changed, not the model's learned parameters.

## Keeping the guide current

Use [CONVENTIONS.md](../CONVENTIONS.md) when preparing a session. When the
first session lands, update the tree, the status table, and the progress in the
[README](../README.md). Mark `src/` present only when it contains demo code.
