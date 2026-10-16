---
name: start-work
description: Use at the start of a work session in any repo under C:\working, before editing files, or when the user says "start work", brings a concept, requests a fresh start, or asks which branch to use. Safely selects the day branch (carrying unmerged earlier-day work forward, never dropping it), loads minimal repo state, and agrees the next step, verification, and relevant README badge/diagram checks with Swamy before implementation.
---
<!-- Managed by engineering-governance. Do not edit here; edit in engineering-governance and run scripts/sync-governance.ps1. -->

# Start work

## 1. Pick the branch

- Check the repository root first; do not infer it from a multi-root workspace or an open editor.
- `C:\working` itself has no remote: stay on `master` and go to step 2.
- Today's branch is `swamy/<ddmmm>-work`: two-digit day, lowercase English month (for example `swamy/05oct-work`).
  - Bash: `LC_ALL=C date +%d%b | tr '[:upper:]' '[:lower:]'` (without `LC_ALL=C`, a non-English locale gives names like `12okt`)
  - PowerShell: `(Get-Date).ToString('ddMMM', [cultureinfo]::InvariantCulture).ToLower()`
- Already on today's branch: go to step 2.
- Run `git status -sb`. If there are uncommitted changes, stop and ask the user before switching branches.
- Run `git fetch --prune --quiet`.
- If a Git or GitHub command fails, report the error and stop branch selection; do not treat missing evidence as "no unmerged work".
- If today's branch exists locally, `git switch` to it. If it exists only on `origin`, `git switch` to it (this tracks the remote).
- Otherwise decide the base. Never cut from `origin/main` until every earlier day branch is proven merged.
  1. List earlier day branches, local and remote, counting `swamy/x` and `origin/swamy/x` once:

     ```bash
     git for-each-ref --format='%(refname:short)' refs/heads/swamy/ refs/remotes/origin/swamy/ | sed 's#^origin/##' | sort -u
     ```

  2. For each branch `x`, use the local ref if it is ahead of `origin/x` (or has no remote), otherwise `origin/x`.
     If local and `origin/x` have diverged, stop and ask. Note any commits that exist only locally (`git rev-list --count origin/x..x`).
  3. Drop `x` as merged only if one of these holds:
     - `git rev-list --count origin/main..x` is `0` (tip is in `main`).
     - A merged PR's head commit equals the tip, which covers squash merges:
       `gh pr list --head swamy/x --state merged --json headRefOid --jq '.[].headRefOid'` prints `git rev-parse x`.
       Commits made after that PR's head are unmerged.
  4. Among the rest, drop any branch that is an ancestor of another remaining one (`git merge-base --is-ancestor a b`). Stacked branches count once, as their tip.
  5. Decide:
     - None remain: `git switch -c <today> --no-track origin/main`
     - One remains: `git switch -c <today> --no-track <that tip>`, and tell the user the new branch carries its unmerged commits.
     - More than one: ask the user which tip to start from. Name each and say which are stacked or unpushed.

  `--no-track` matters: without it the new branch tracks `origin/main` (or the earlier branch), so a later `git pull` pulls from that branch and `git push` fails on the name mismatch.
  The first push, when the user asks for one, is `git push -u origin HEAD`.
- Report merged earlier branches that are still present locally and offer to delete them. Delete only when the user says yes; a squash-merged branch needs `git branch -D`.
- Report any unpushed commits found in step 2. Do not push them unless the user asks.

## 2. Load the state

Read only what tells you where things stand:

- `git status -sb` and `git log --oneline -5`
- Open plans in `docs/plans/` (most recent first; skip plans whose status says `State: done`). Read the "Next" and "Blockers" lines.
- The README progress or status section.

Treat plans as a starting point, not proof: reconcile their branch, completed steps, and blockers with the current worktree. Do not read every historical plan or private memory file.

## 3. Agree the next step with Swamy

- Swamy brings the concept; Swamy and AI develop it together. Use an already explicit request or recorded agreement when it covers the current step; do not ask for the same agreement again.
- If no concept is supplied, ask Swamy and wait. A backlog, suggested kata, or stack default does not authorize implementation.
- Before new scaffolding or code, clarify the concept's scope and examples, agree the language/stack and one small next step, and define its acceptance check.
- When the step changes documentation, include exactly seven distinct badges with seven different medium-tone colors in every affected README and pair useful Mermaid diagrams with equivalent ASCII fallbacks. Do not claim unimplemented tooling in badges.
- For a fresh start, inventory the files and agree exact deletion boundaries before removing anything. Preserve Git history, governance infrastructure, and unrelated work unless explicitly included.

## 4. Report

Three lines at most: branch (and where it came from, if new), uncommitted changes, and the agreed next step with its acceptance check (or "awaiting Swamy's concept").
