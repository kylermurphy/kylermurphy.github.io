---
title: "CONTIGO: satellite-derived atmospheric density from orbits"
kicker: "Orbit mechanics · Scientific software"
excerpt: "A modular framework that turns spacecraft orbit data into energy dissipation rates and effective atmospheric density, validated against the Orekit flight-dynamics library."
collection: portfolio
order: 2
featured: true
image: "/images/portfolio/contigo.png"
header:
  teaser: "portfolio/contigo.png"
tags_list: ["Python", "Orekit / Java", "SPICE", "Software architecture"]
links:
  - label: "GitHub"
    url: "https://github.com/kylermurphy/contigo_edr"
---

<img src="/images/portfolio/contigo.png" alt="CONTIGO: satellite-derived atmospheric density from orbits" style="max-width:100%; border-radius:6px; margin-bottom:1em;">

Precise orbit data from LEO satellites (including whole constellations) carries a signature of atmospheric drag. CONTIGO extracts it: it computes the energy dissipation rate (EDR) of each spacecraft and converts it into an effective density that can be used to validate or drive density models.

**Highlights**

- **Plug-in physics.** Every force (gravity field, third-body, solar radiation pressure, …) implements a common `ForceModel` protocol, so new forces drop into the core `EDRDensity` calculation without touching it.
- **Flexible data layer.** `Spacecraft` and `Constellation` classes load HDF, CSV, and SP3 orbit files (zipped or not) and normalize them into one internal state.
- **Fast ephemerides.** Choice of SPICE or Orekit, plus a quantized, lazily loaded ephemeris cache shared across a constellation and a small Java helper that batches Orekit calls.
- **Validated.** Energy terms agree with Orekit's independent computation (figure above).

[GitHub](https://github.com/kylermurphy/contigo_edr)
