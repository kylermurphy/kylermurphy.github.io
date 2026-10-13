---
title: 'mastersbasketball.ca, Part 2: A Score Sheet Built for AI to Read'
date: 2026-10-13 09:00
permalink: /posts/2026/10/post-15/
tags:
  - claude
  - claude code
  - ai workflows
  - computer vision
  - basketball
---

[Part 1](/posts/2026/10/post-14/) covered designing and building the league's website. This
part is about where its numbers come from. Games are scored on paper by a volunteer, and
someone has to turn each sheet into stats. That someone is me this year, but it might not be
next year, and they might not have a paid AI subscription or write any code.

The answer we landed on: **redesign the paper sheet so a photo of it can be read reliably,
let AI turn the photo into a draft that flags every box it isn't sure of, and have a person
clear those flags against the paper before anything is published.** The AI saves the typing.
The person decides what's true.
{: .notice--primary}

{% include toc title="Contents" icon="file-text" inline=true %}

## The score sheet

<img src="/images/portfolio/masters-basketball/score-sheet.png" alt="A filled-in practice score sheet: two rosters with free-throw circles and foul boxes at the top, quarter scores, a notes box, and the running score in five columns below" style="max-width:100%; margin-bottom:1em;">

This is a practice game with made-up players. The sheet went through several versions in
one morning of back and forth with Claude, and the first one didn't work. It had a points
total box for each player, to be added up at the end of the game. Points need to be tied to a
player as they're scored, so I pushed for the format other score sheets use: the score down
the middle, each team on one side.

The design we settled on keeps the scorekeeper's job close to what they already do:

- **A running score.** The totals run down the middle of each column, and the scorekeeper
  writes the scorer's jersey number in that team's box beside the new total. The jump from a
  team's previous total gives the basket's value and who scored it. No adding up.
- **Free throws in the player's row.** Ten circles each: fill one for a make, slash one for a
  miss. Under league rules a free throw can be worth more than one point, so the circles, not
  the running score, are the record of free throws.
- **Here ticks** for games played, five foul boxes and two red **T** boxes for technicals.
- **Quarter boxes** for the running total at the end of each quarter, and a **Notes** box
  for flagrant fouls.
- **Page 2 on the back** carries the running score past 100 and free throws past ten, so
  the front stays big and clear.
- **Black squares in the four corners**, so a photo taken at an angle can be straightened.

It prints in four layouts (portrait or landscape, Letter or Legal) and the scorekeeper picks.
Before each game day, the site generates that night's sheets with the date, teams, game IDs
and both rosters with jersey numbers already printed, and links them from the schedule.
Every printed name stays an editable PDF field for last-minute changes.

## One spec for everything

The sheet kept changing, and it will keep changing. So every structural number on it (rows,
circles, foul boxes, score boxes, how many points a page holds) lives in one place, a `SPEC`
in the Python script that draws the PDF. The script also writes that spec out as JSON, and
everything else is built from it:

- **The game file** is a box-for-box copy of the sheet in YAML: who was here, each free-throw
  circle, fouls, the quarter boxes, and the running score as "total → jersey number". No
  totals are typed in; the build works out points, free throws made and attempted, and games
  played from the boxes.
- **The rules** (in Python) check a game file and return each problem with a path to one
  box: the last running total must match the Final box, each quarter box must match the
  running total at that quarter's line, every scorer's number must be on the roster and
  ticked Here.
- **The entry page** (below) draws its copy of the sheet from the spec, and runs a
  JavaScript port of the same rules as you type. Both versions run against the same set of
  test game files on every deploy, so they can't drift apart.

## From photo to draft

There are three ways to get a draft, and the rest of the workflow doesn't care which one was
used.

**With Claude Code**, a `/record-game` command does it in five steps:

1. **Measure, with no AI.** A script finds the four corner squares, straightens the page,
   works out which layout and which game it is by matching every scheduled game's printed
   sheet, then subtracts that printed sheet from the photo so only pen is left. It measures
   the ink in every box: how much of a tick box is filled, and whether a free-throw mark is a
   slash (long and thin) or a fill (round and solid).
2. **Read.** Claude reads only the handwriting: the jersey numbers in the running score, the
   score boxes, any player written in by hand. Every number is checked against the team's
   roster.
3. **Read the running score twice.** A second, independent reading (a Sonnet subagent) runs
   alongside, and every box where the two disagree gets another look. This is for the one
   mistake no rule can catch: a number read as another number on the same roster.
4. **Check** the draft with the site's rules, and flag the box most likely behind each error.
   It copies the paper, never corrects it: a wrong Final box is written as is, and flagged.
5. **Save** the draft and the photo to the repo, and finish with a link that opens the draft
   for checking.

**Without Claude Code**, the entry page has a **Copy the prompt** button: a prompt for the
free claude.ai or ChatGPT that reads the photo section by section and writes a draft in the
same format. Nothing measures the ink, so expect more flags.

**Without AI at all**, the same page starts an empty sheet with the rosters filled in, and
someone types it in.

### How well it reads

So far it's been tested mostly on made-up photos: four practice games drawn onto all four
layouts, then "photographed" with tilts, perspective, shadows, blur and JPEG noise. A box is
**right**, **flagged** (wrong or unsure, but flagged, so a person looks) or **wrong**
(wrong and not flagged, the failure that matters).

| Test | Boxes | Right | Flagged | Wrong |
|---|---|---|---|---|
| Measuring step, normal photos | 1,512 | 100% | 0 | 0 |
| Measuring step, hard photos | 1,512 | 99.0% | 15 | 0 |
| Whole command, four hardest photos (Opus reading) | 751 | 743 | 7 | 1 |

The one wrong box was a faint foul slash on the blurriest photo, and the threshold has since
been lowered so it's flagged. An earlier miss taught the most: on a blurry photo, two readers
swapped 46 and 48, two players on the same team, both marked Here. No rule can catch that,
which is why the running score is now read twice and look-alike numbers on each roster are
listed for the reader.

The first real photo, a practice sheet filled in by hand and photographed on a table, needed
four fixes to the measuring step, including a corner square right at the photo's edge and a
dark table edge mistaken for a corner. Real paper is always the better test.

## The person in charge

<img src="/images/portfolio/masters-basketball/entry-page.png" alt="Three phone screens of the score sheet entry page: the checks panel listing two flags, the running score with one flagged box outlined, and the save panel" style="max-width:100%; margin-bottom:1em;">

The checking happens on an unlisted page on the site itself, so it needs no account, no
install and no subscription. It's a working copy of the paper sheet:

- **Open a draft** (or a file, or a game from the schedule) and the photo beside it. The
  photo stays on your device.
- **Flags are highlighted** on their box with the reader's note ("22 or 54?", "filled or
  slashed? hard to read"). Compare with the paper, fix if needed, and **Mark as checked**.
- **The checks run as you type.** Errors in red, flags in blue, warnings dashed, and a panel
  with each player's points and free throws as the sheet works them out.
- **Save as final** stays greyed out until there are no errors and no flags. It then opens
  GitHub's new-file page with the game file filled in, as a pull request. The site's build
  runs the same checks again, and merging publishes the game.

A draft never reaches the site by itself. The job shrinks from copying 190 boxes to looking
at a handful, but a person still signs their name to every game.

## What I'd take from this

- **Design the input, not just the reader.** A fixed layout, corner squares and pre-printed
  rosters did more for accuracy than any prompt. Most of the work is a plain script; the AI
  only reads handwriting.
- **Make the AI's doubt part of the data.** Flags live in the draft file, point at one box,
  and block saving until a person clears them.
- **Count the silent mistakes.** "Wrong and not flagged" is the number that matters, and
  every one found so far changed the design.
- **Keep a way in for everyone.** Claude Code, a free chat, or typing by hand all end on the
  same page with the same checks, so the workflow outlives whoever runs it this year.

The season's first real sheets are still to come. I'll find out how much of this survives a
scorekeeper's actual handwriting at the end of a long night.
