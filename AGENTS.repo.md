# Repo-specific rules

- Each session lives in `sessions/<yyyy-mm-dd>-<topic>/` with a `notes.md` (agenda, questions, answers, follow-ups); add `slides/` or `demos/` only when the session has them.
- Record questions without attendee names unless they agree to be named. No secrets, credentials, or customer data. This repo is public.
- Do not create a session folder until Swamy agrees its topic and scope.
- Check all maintained Markdown before committing: `npx --yes markdownlint-cli2@0.23.3` from the repo root (Node.js 22+).
- Before task edits, read repo-root `CONVENTIONS.md` and relevant `CORRECTIONS.md` entries. Check `SESSION_STATE.md` for overlapping work; it is advisory, not a lock.
- Repo-root `HANDOFF.md` indexes unfinished plans; `memory.md` indexes durable knowledge. Load their linked details only when relevant; neither replaces Git, the README, or shared governance.
