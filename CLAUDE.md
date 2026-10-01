# CLAUDE.md — kylermurphy.github.io

Instructions for Claude Code **and** claude.ai/code (cloud) sessions working in this repo.
Both read this file. Edit it in dev-hub (`repos/kylermurphy.github.io/CLAUDE.md`), not
here: this copy is replaced from the master at the start of each task.

## What this is
Kyle Murphy's academic personal site, built on the **Academic Pages** Jekyll template
(GitHub Pages). Publications, talks, teaching, CV, portfolio, and a talk map.

## Environment & build
- Jekyll site. Local build: `bundle install` then `bundle exec jekyll serve` (Ruby +
  Bundler; `Gemfile` / `Gemfile.lock` present).
- Content lives in Markdown under `_pages/`, `_posts/`, `_publications/`, `_teaching/`,
  `_portfolio/`. Site config in `_config.yml` (dev overrides in `_config.dev.yml`).
- `markdown_generator/` + `talkmap.py` / `talkmap.ipynb` generate publication/talk pages
  and the talk map from data files.

## Commands
- No test suite (content site). Verify by building locally and checking pages render.

## Conventions & gotchas
- Add publications/talks via the data files + `markdown_generator`, not by hand-editing
  generated pages where a generator exists.
- `Gemfile.lock` and JS deps drift over time (task **SITE-2**) — refresh periodically.

## Learnings

Durable facts from past tasks, promoted from `log/<ID>.md` by `mark-done` (max ~15).

_None yet._

## Task protocol (dev-hub tasks)

Tasks come from **dev-hub** (`kylermurphy/dev-hub`). Its `CLAUDE.md` → **Task protocol** is the
full, authoritative version; this is the summary. Each task is self-contained: start from its
board row alone.

- **Branch** `task/<ID>-<slug>` off the default branch; never commit to `main`.
- **First commit:** sync this file from its dev-hub master
  (`repos/kylermurphy.github.io/CLAUDE.md`). Edit instructions in the master, never here.
- **Plan** saved to dev-hub `log/<ID>.md` before heavy work, naming who does each step (main
  model or a subagent). `plan-task <ID>` discusses it and **waits for Kyle's go**;
  `run-task <ID>` plans and runs without waiting, stopping only under dev-hub `CLAUDE.md` →
  When to stop and ask. A `plan <ID>` dry run saves nothing. **Draft PR** following dev-hub's `templates/PULL_REQUEST_TEMPLATE.md`
  (not copied here): ID, what, why, how tested, DoD check.
- **Bookkeeping** (`log/<ID>.md`, `TASK_LOG.md` row, board Status → `WIP`) goes straight to
  dev-hub `main`. In a branch-restricted session it goes to the designated branch with an
  open PR instead (say so in chat; never merge it yourself). Only `mark-done <ID>` sets `Done`.
- **Stop states:** `Blocked` (fill `## Blocked / open questions`) or `Usage-stopped`; keep
  `Next step` current and resume with `pickup-task <ID>`.
- **Batches** (`multi-task`, or `plan-task` with several IDs): one branch
  `task/<ID>+<ID>+…-<slug>` and one PR for up to 5 simple tasks; each keeps its own log, and
  commits are prefixed with their ID. A `Blocked` task is dropped from the batch; the rest
  ship. Rules: dev-hub `CLAUDE.md` → Batches.
- **Features** (dev-hub `FEATURE_BOARD.md`): larger work on one long-lived branch
  `feature/<ID>-<slug>` (IDs like `<PREFIX>FA`). Its subtasks (`<PREFIX>FA1`, …) are committed
  straight onto it, each commit prefixed with the subtask ID, after merging the default branch
  in; one draft PR into `main` carries the whole feature. Rules: dev-hub `CLAUDE.md` → Features.
- **Learnings:** mark lasting findings as `Learning:` lines in the log; `mark-done` promotes
  them into `## Learnings` above (via the master).
- **Subagents:** delegate only broad/mechanical work to cheaper models, per dev-hub
  `CLAUDE.md` → Subagents; the main session does all commits and pushes.
- Build locally (`bundle exec jekyll serve`) and check pages render before the PR.
- Definition of done = the task's row on dev-hub `TASK_BOARD.md`.

## Task board
This repo's backlog IDs use the **`SITE-`** prefix.
