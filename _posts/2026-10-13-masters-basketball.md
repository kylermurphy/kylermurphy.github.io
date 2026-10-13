---
title: 'mastersbasketball.ca, Part 1: Designing and Building a League Site with Claude'
date: 2026-10-13 08:00
permalink: /posts/2026/10/post-14/
tags:
  - claude
  - claude code
  - web
  - jekyll
  - basketball
---

I play in a masters basketball league in Thunder Bay: five teams, about ten players each,
games from October to April and playoffs in April. Games are scored on paper, and there was
no website. Nobody could check the standings, the schedule or who's leading the league in
scoring without asking around.

So I built one: [**mastersbasketball.ca**](https://mastersbasketball.ca/). It has standings,
the schedule, box scores, player and team pages, and an archive of past seasons, all made
for phones. I designed it in Claude and built it with Claude Code, and it costs nothing to
run beyond the domain.
{: .notice--primary}

This is part 1 of two. It covers the design and the build. [Part 2](/posts/2026/10/post-15/)
covers the part I find more interesting: a paper score sheet built to be read by AI, and a
workflow where a person checks every flagged box before a number goes live.

{% include toc title="Contents" icon="file-text" inline=true %}

## What the site does

The screenshots here come from the site's preview copy, which runs on made-up sample data
(the banner under the header says so). The real season's pages look the same.

<img src="/images/portfolio/masters-basketball/home-light-dark.png" alt="The home page on a phone, in the light theme and the dark theme" style="max-width:100%; margin-bottom:1em;">

The **home page** has the latest results, the next game day and the standings. The header is
the Sleeping Giant, the rock formation across the bay from Thunder Bay, with a rising sun in
the light theme and a setting moon in the dark one. The site follows the phone's own theme,
and the sun/moon button switches it.

<img src="/images/portfolio/masters-basketball/stats-player-boxscore.png" alt="Three phone screens: the player stats page with one player's row opened, a player page with points by game day, and a box score" style="max-width:100%; margin-bottom:1em;">

**Stats** ranks players by points per game, total points or free-throw percentage, filtered by
team. Tapping a player opens their free throws, season high and points by game day, with a
link to their own page. Every game has a **box score**: the score by quarter and each
player's points and free throws.

<img src="/images/portfolio/masters-basketball/schedule-team-archive.png" alt="Three phone screens: the schedule with the next game day highlighted, a team page with its roster, and a past season in the archive" style="max-width:100%; margin-bottom:1em;">

The **schedule** highlights the next game day and links each upcoming night's score sheets
(more in part 2) and team calendars. **Team pages** have the record and a ranked roster, and
the **archive** keeps every past season's final standings and leaders.

A few rules shaped everything:

- **Players appear as "First L."** ("#54 Dave M."), never full names, photos or contact details.
- **No analytics, no trackers, and no search engines.** The league didn't want the site on
  Google, so every page asks not to be indexed.
- **Nothing invented.** Where the league hasn't decided something yet (a tiebreaker, a
  playoff matchup), the site shows a visible placeholder and the question goes on a list.

## Designing it in Claude

I started in a regular Claude chat, before any code. I described the league, the pages I
wanted and who would use them (players, on their phones), attached the league's existing
logo, and asked for five different visual directions to look at in the morning. Claude laid
them out as phone mockups on a design canvas: a classic club look, a night theme, a Lake
Superior theme, a scoreboard style and a box-score style.

None was quite it, so I asked for its own recommendation as a sixth, and liked it. From there
the changes were the kind you'd make with a designer:

- **The Sleeping Giant.** Its first silhouette was wrong, so I sent a photo of the real
  skyline and it traced the outline from that.
- **Two themes.** A sunrise for light, a setting moon for dark, and the dark sky lightened
  so the Giant stays visible.
- **The logo.** The old logo had a banner and small text that turn to mush at phone size. We
  simplified it into a round badge (the basketball, MASTERS and the maple leaf), plus a
  wordmark and an "M in a basketball" icon that reads at favicon size.
- **A brand kit.** Colours for both themes with contrast checked, fonts (Barlow and Barlow
  Condensed), and the logo files the site would need.

Then a desktop version of the home page, and Claude packaged everything Claude Code would
need to build it into one zip: the mockups as HTML and PNG, the brand kit, a design brief
for every page (including the ones never mocked up), and a `CLAUDE.md` with the rules.

## Building it with Claude Code

I created a GitHub organization for the league, unzipped the package into an empty repo, and
built the site with Claude Code on the web in a series of short sessions, one per step,
reviewing screenshots after each:

1. **Scaffold** (Opus): the Jekyll site, the deploy workflow, the stats script and a
   believable fake season to build against.
2. **Header, footer, theme switch and home page** (Sonnet), matched to the mockups.
3. **Stats**, and a sample-data switch with a banner, so the site could go live before the
   first real game.
4. **Every other page**: schedule, teams, players, box scores, archive, 404.
5. **A full check** (Opus): every page at 360, 390 and 1440 px, in both themes, for
   sideways scrolling, contrast and anything that didn't match the mockups.

Then the domain: registered at Porkbun, verified on the GitHub organization, and pointed at
GitHub Pages.

The first commit was October 8. By October 13 there were 26 merged pull requests, a good share
of them the score sheet work in part 2. A few things made that pace possible.

**The handoff files did the remembering.** Each Claude Code session starts fresh. The
`CLAUDE.md`, the design brief and the mockups in the repo meant every session knew the rules
(colours only from the brand variables, nothing wider than a phone screen, "First L." names)
without me repeating them.

**Data in plain text files.** Seasons, teams, players, the schedule and each game are small
YAML and CSV files in the repo. A Python script checks them and works out every number, and
Jekyll turns the numbers into pages. If a check fails (a score that doesn't add up, an
unknown player), the build stops with a plain message and nothing is published.

**A preview copy with fake data.** Every deploy also builds the whole site from a made-up
season into a hidden preview, so changes can be tried with realistic numbers while the real
season is empty. It's where these screenshots come from.

**Screenshots as the review.** Claude Code took phone and desktop screenshots in both themes
after each step, and a script checks every page for sideways scrolling, console errors and
broken links. I reviewed pictures, not diffs.

## What I'd tell someone trying this

- **Design first, in a chat, before any code.** Choosing between finished-looking mockups
  is quick, and every later session builds toward a picture instead of a description.
- **Write the rules down in the repo.** A good `CLAUDE.md` and design brief turn a run of
  separate sessions into one consistent build.
- **Keep the steps small and look at every one.** One session per step, a screenshot at the
  end, and a pull request I could read.
- **Let the computer refuse bad data.** Checks that stop the build matter more than any
  page design when volunteers will be editing the data.

In [part 2](/posts/2026/10/post-15/): the score sheet, and how a photo of it becomes stats
with a person checking every doubtful box.
