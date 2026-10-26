---
title: "mastersbasketball.ca: a league website, from paper score sheets to stats"
kicker: "Web · AI workflows"
excerpt: "A phone-first site for a Thunder Bay masters basketball league, designed in Claude and built with Claude Code, with a printed score sheet that AI reads into a draft and a person checks before anything is published."
collection: portfolio
order: 10
featured: false
image: "/images/portfolio/masters-basketball/masters-basketball.png"
header:
  teaser: "portfolio/masters-basketball/masters-basketball.png"
tags_list: ["Claude Code", "Jekyll", "Python", "Human-in-the-loop AI"]
links:
  - label: "Site"
    url: "https://mastersbasketball.ca/"
  - label: "Write-up, part 1"
    url: "/posts/2026/10/post-14/"
  - label: "Write-up, part 2"
    url: "/posts/2026/10/post-15/"
---

<img src="/images/portfolio/masters-basketball/masters-basketball.png" alt="Three phone screens from the league site: the home page, the player stats page in dark mode, and the score sheet entry page with a flagged box" style="max-width:100%; border-radius:6px; margin-bottom:1em;">

A masters basketball league in Thunder Bay scores its games on paper and had no website: no standings, schedule or player stats that players could check on their phones.

**What I did**

- Designed the site in Claude: five visual directions, then one, with a Sleeping Giant skyline traced from a photo, a sunrise light theme and a moonset dark theme, and a simplified round logo and brand kit.
- Built it with Claude Code in short, reviewed steps: a static Jekyll site with a Python stats step, deployed by GitHub Actions to GitHub Pages. Standings, schedule, box scores, player and team pages, and an archive, all built for phones.
- Designed a printed score sheet so a photo of it can be read reliably: a running score that gives every point to a jersey number, free-throw circles, and corner squares to straighten the photo. One spec drives the PDF, the data checks and the entry page.
- Made the AI step a draft, never the answer: a photo becomes a draft with every doubtful box flagged, and a person clears the flags on an entry page that checks the sheet as they go. Nothing reaches the site until the checks pass.

**Outcome:** The site is live for the 2026-27 season and costs nothing to run beyond the domain. A volunteer can keep it up to date with Claude Code, with a free chat assistant, or by typing a sheet in by hand.

[Site](https://mastersbasketball.ca/) · [Write-up, part 1](/posts/2026/10/post-14/) · [Part 2](/posts/2026/10/post-15/)
