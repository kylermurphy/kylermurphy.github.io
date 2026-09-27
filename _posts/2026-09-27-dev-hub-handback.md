---
title: 'dev-hub Handback Mode: Running Tasks from a Claude Project'
date: 2026-09-27
permalink: /posts/2026/09/post-11/
tags:
  - claude
  - ai agents
  - workflow
  - github
---

In my [last post](https://kylermurphy.github.io/posts/2026/09/post-10/) I described
**dev-hub**, a private GitHub repo that acts as mission control for Claude across my repos. Most
of the time I run dev-hub tasks from Claude Code, either on my machine or on the web, where
Claude can push branches and open pull requests itself.

I also wanted a way for people without Claude Code to use `dev-hub`. **Handback mode** covers
that case. It's a claude.ai Project with dev-hub added as a read-only source and a set of custom
instructions pasted in. Claude can't push anything from there, so it does the work and *hands it
back*: a patch per repo and the PR text. Once you confirm the PR, Claude marks the task done,
keeping its own bookkeeping, and you then apply the patches, push, and open and merge the PR.

This post covers setting it up, running a task and applying the handback. The bookkeeping
details are under *Going further*, as optional reading.

{% include toc title="Contents" icon="file-text" %}

## Set it up

Setup is a one-time job of about ten minutes.

1. **Create a Project** in claude.ai.
2. **Connect GitHub.** In claude.ai, open **Settings → Connectors** and connect GitHub. Then, on
   GitHub, install the [Claude GitHub App](https://github.com/apps/claude) on your dev-hub
   repo. dev-hub is private, so the Project can't see it without the app.
3. **Add dev-hub to the Project's files.** In the Project, open **Files**, add a GitHub source,
   and pick dev-hub: branch `main`, the whole repo. This is the Project's knowledge. Claude
   reads the board, the rules and the logs from it, but it can't write back.
4. **Paste in the instructions.** Copy
   [`templates/PROJECT_INSTRUCTIONS.md`](https://github.com/kylermurphy/dev-hub-template/blob/main/templates/PROJECT_INSTRUCTIONS.md)
   into the Project's custom instructions. They tell Claude to follow dev-hub's normal rules,
   with a few substitutions for not being able to push.
5. **Optional: turn on automatic approval** of actions for the Project, so chats don't stop to
   ask before each tool call.

To check it works, start a chat in the Project and type `how-to`. Claude prints a short guide
to the loop below.

Then add your repos to the task board with `add-repo <owner>/<repo>`, `refresh-overview`, then
`scan-repo <name>`:

- Claude hands back a patch for the `dev-hub` repo with the updated task board.
- Apply the patch on the `chore/` branch named in the PR text (see
  [Applying the handback](#applying-the-handback)), then open and merge that PR, and you're
  good to go.

## Running a task

The commands are the same as in the rest of dev-hub: `plan-task`, `multi-task`, `scan-repo` and
so on. A task goes like this:

1. **Name the task**, e.g. `do task COOK-8`.
2. **Claude runs two checks** before doing anything: whether any earlier task was left
   unfinished (flagged with 🚩), and whether dev-hub has changed since the last run.
3. **Claude does the work.** It clones the target repo, makes the changes, tests what it can,
   and shows me the PR text.
4. **Claude keeps dev-hub's bookkeeping.** A Project can't push or open PRs, so Claude can't
   update dev-hub's task log and board directly. Instead it tracks them in the Project itself
   and hands them back with the work. See [The working copy](#the-working-copy) for how.
5. **I reply "looks good".** Claude runs `mark-done` and hands back one `.patch` per repo, plus
   a zip for each.

Here's what that looked like for COOK-8, which fixed two typos in recipe URLs on my recipe site:

```
me:     do task COOK-8
Claude: No unfinished work · dev-hub unchanged since 2026-09-25.
        … renames both recipes, adds redirects from the old URLs …
        Here's the PR for smurphs_cooking. Look good?
me:     looks good
Claude: Running mark-done COOK-8.
        Handback: smurphs_cooking-COOK-8.patch, dev-hub-COOK-8.patch
```

There are two patches because a task touches two repos: the code change goes to the target
repo, and the bookkeeping (the task log and the board status) goes to dev-hub.

## Applying the handback

A task comes back as **two handbacks**, a patch and a zip for each repo it touched:

- **the target repo** (e.g. `smurphs_cooking-COOK-8.patch`): the code change, applied on a new
  branch and opened as a PR;
- **dev-hub** (e.g. `dev-hub-COOK-8.patch`): the bookkeeping (task log, `TASK_LOG.md` row and
  board status), applied straight to `main`.

Each patch holds real commits, with their messages, not just the changed files. So applying one
is a single `git am` command. Repeat these steps for each patch. I use GitHub Desktop:

1. **Open the repo** and pull `main`.
   - Target repo: create the branch named in the PR text, from `main`.
   - dev-hub: stay on `main`, since the bookkeeping goes straight there.
2. **Open a command line:** Repository → **Open in Command Prompt**.
3. **Apply the patch:**
   - Target repo, on the new branch:

     ```
     git am path_to_patch/smurphs_cooking-COOK-8.patch
     ```

   - dev-hub, on `main`:

     ```
     git am path_to_patch/dev-hub-COOK-8.patch
     ```

4. **Push**, and for the target repo, open the PR using the text Claude gave you.
5. **Re-sync the Project's dev-hub source**, so the next chat sees the change. The next chat's
   checks confirm it landed.

If `git am` fails, run `git am --abort` to clean up, and upload the changed files from the zip
instead. A leftover "previous rebase directory still exists" error has the same fix.

## Good to know

- **Keep each chat to one repo.** Several chats can run at once, but two chats on the same repo
  can overwrite each other's work. For several tasks in one repo, use `multi-task` in a single
  chat.
- **Target repos must be public.** Claude clones them anonymously, so a private target repo
  can't be worked on here. (dev-hub itself can be private; it comes in through the Project's
  files.)
- **Some builds and tests can't run.** The Project's sandbox blocks some package registries.
  For COOK-8, Claude couldn't install the Ruby gems to build the Jekyll site, so it checked what
  it could and left the build checks in the PR for me to run before merging.
- **Only finished work is handed back.** If a task stops partway, Claude says so, and every
  later chat flags it with 🚩 until it's resolved.
- **Re-sync dev-hub regularly.** The Project's copy of dev-hub doesn't update itself. Re-sync
  its GitHub source in the Project's files after you apply a handback, and whenever dev-hub
  changes elsewhere. The next chat spots the new copy, clears the Project's internal
  bookkeeping for everything that has landed, and starts fresh from it. See
  [The sync check](#the-sync-check) for how.

## Going further (optional)

The sections below cover how handback mode keeps its books without being able to push.

### The working copy

<div class="notice" markdown="1">

Normal dev-hub sessions commit bookkeeping straight to dev-hub's `main`. A Project can't, so it
keeps a **working copy** in the Project's own docs, under `wc/`:

- `wc/dev-hub/<path>` stands in for dev-hub `main`. A file is copied in the first time it
  changes, and Claude reads `wc/` first and the synced repo otherwise.
- `wc/<repo>/<branch>/` holds a target-repo branch as patches plus a `PR.md`. Claude rebuilds
  the branch by cloning the repo and applying them.
- Every chat in the Project shares the working copy, which is why two chats on the same repo
  can collide: Project docs are replaced whole, not merged.

Claude can only read the synced dev-hub in fragments, so the first working copy of a file is
rebuilt from those pieces. The handback flags such files, and it's worth checking GitHub's diff
shows only the intended changes.

</div>

### The ledger

<div class="notice" markdown="1">

`wc/LEDGER.md` is the Project's record of what's been done. It has two parts:

- **Sync snapshot:** the date of the last check and the document ID of every synced dev-hub
  file.
- **Log:** one row per action, with a status: `in progress`, `stopped` and
  `awaiting confirmation` are unfinished; `handed back` and `synced` are done.

The unfinished statuses are what the 🚩 check at the start of each chat looks for.

</div>

### The sync check

<div class="notice" markdown="1">

The second check at the start of each chat compares the snapshot's document IDs with the
current ones. A changed ID means that file's content changed. If nothing changed, Claude says
so in one line and carries on. If something did, it checks, before running anything, that:

- **handbacks landed:** handed-back work now in the synced repo has its `wc/` files deleted and
  its rows set to `synced`;
- **outside edits merge:** a file I edited on GitHub that also has pending `wc/` edits gets
  merged, or waits for me if it can't be merged cleanly;
- **the rules still agree:** if `CLAUDE.md`, `COMMANDS.md` or the templates changed, Claude
  summarizes the new rules and flags anything pending that no longer follows them;
- **the board is consistent,** using the same checks as `check-board`.

</div>

### Closing a task without a merge check

<div class="notice" markdown="1">

Normally `mark-done` checks that the PR merged before setting `Done`. Here I open and merge the
PR myself, after the handback, so Claude can't check it. My "looks good" stands in for the
merge check. The task log records `Done (PR confirmed <date>)` instead of
`Done (merged <date>)`, and dev-hub gets one bookkeeping commit instead of separate `WIP` and
`Done` commits.

"PR confirmed" isn't "merged", though. If a later sync check finds a confirmed task whose
change never reached the target repo's `main`, it flags it. I then merge the PR, or reopen the
task with `pickup-task`.

</div>

### What's in a handback

<div class="notice" markdown="1">

One zip per repo, holding:

- the changed files at their repo paths;
- the `.patch`;
- the PR text and branch name (target repo), or the commit message (dev-hub bookkeeping);
- a list of files to delete, if any;
- a `README.md` with the `git am` steps, using the real branch and patch names.

Each patch is also sent on its own, named `<repo>-<ID>.patch`, so you can grab it without
opening the zip.

</div>
