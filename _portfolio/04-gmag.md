---
title: "GMAG: ground magnetometer data and induced electric fields"
kicker: "Open-source · Data engineering"
excerpt: "An open-source package that downloads and loads data from several ground-magnetometer arrays into one pandas interface, now with tools to compute geoelectric fields for space-weather hazard work."
collection: portfolio
order: 4
featured: true
image: "/images/portfolio/gmag.png"
header:
  teaser: "portfolio/gmag.png"
tags_list: ["Python", "pandas", "Data pipelines", "Geomagnetically induced currents"]
links:
  - label: "Paper"
    url: "https://doi.org/10.3389/fspas.2022.1005061"
  - label: "Docs"
    url: "https://kylermurphy.github.io/gmag/"
  - label: "GitHub"
    url: "https://github.com/kylermurphy/gmag"
---

<img src="/images/portfolio/gmag.png" alt="GMAG: ground magnetometer data and induced electric fields" style="max-width:100%; border-radius:6px; margin-bottom:1em;">

Ground magnetometer data are spread across many networks with different formats and servers. GMAG hides that complexity: one call downloads and loads data from CARISMA, CANOPUS, IMAGE, THEMIS and other arrays into a pandas DataFrame.

- A [documentation site](https://kylermurphy.github.io/gmag/) with examples, [per-array details](https://kylermurphy.github.io/gmag/arrays), a [station map](https://kylermurphy.github.io/gmag/stations), and a [searchable coordinate table](https://kylermurphy.github.io/gmag/cgm_2000.html).
- An `efield` module that computes 1-D surface impedance and the induced geoelectric field from magnetometer data, the quantity that drives geomagnetically induced currents in power grids and pipelines. Resistivity profiles for selected stations are included.
- Described in *Frontiers in Astronomy and Space Sciences* ([2022](https://doi.org/10.3389/fspas.2022.1005061)).

[Paper](https://doi.org/10.3389/fspas.2022.1005061) · [Docs](https://kylermurphy.github.io/gmag/) · [GitHub](https://github.com/kylermurphy/gmag)
