# kylermurphy.github.io

Personal site of Kyle Murphy, built on the [Academic Pages](https://github.com/academicpages/academicpages.github.io) Jekyll template (upgraded to the September 2026 upstream, v0.9.x).

## Where things live

| Content | Location |
|---|---|
| Landing page | `_pages/about.md` |
| CV / résumé | `_pages/cv.md` |
| Portfolio projects | `_portfolio/*.md` (front matter: `order`, `featured`, `kicker`, `image` or `icon`, `tags_list`, `links`) |
| Notes (tips & write-ups) | `_posts/` (listed at `/notes/`) |
| Publications | `_publications/` (generated with `markdown_generator/publications.ipynb`) |
| Header menu | `_data/navigation.yml` |

## Customizations on top of the template

Keep these in mind when pulling a future upstream update:

- `_sass/layout/_custom.scss`: all custom styling (hero, cards, CV layout, code font size, inline TOC, print styles). Imported last in `assets/css/main.scss`.
- `_includes/kyle-card.html`: project card used on the landing and portfolio pages.
- `_includes/archive-single-cv-pub.html`: publication entry for the CV.
- `_includes/author-profile.html`: Google Scholar chart under the sidebar links (shown when `author.scholar: true` in `_config.yml`). Light/dark PNGs are loaded from [scholar_plot](https://github.com/kylermurphy/scholar_plot) (`figures/scholar_light.png`, `figures/scholar_dark.png` on raw.githubusercontent.com); the figure hides itself if they fail to load.
- Live Scholar numbers: `assets/js/scholar.js` (loaded from `_includes/scripts.html`) fetches `data/scholar.json` from scholar_plot and fills any `data-scholar="citations.all"`-style, `data-scholar-since` and `data-scholar-updated` elements. `_includes/scholar-stat.html` renders one number with its build-time fallback from `_data/scholar_fallback.yml` (publications fall back to the size of `_publications`). Used by the landing-page stats and the CV "Research impact" row. Nothing is generated in this repo.
- `_includes/toc`: `inline=true` option for a table of contents in the text column.
- `_layouts/single.html`: `hide_title: true` front-matter option.

## Local preview

```bash
bundle install
bundle exec jekyll serve -l -H localhost
```

Pull requests upload the built site as a `site-preview` artifact (see `.github/workflows/jekyll-build.yml`).
