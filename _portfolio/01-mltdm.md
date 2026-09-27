---
title: "MLTDM: Machine-learning thermospheric density model"
kicker: "Space weather · Machine learning"
excerpt: "A random-forest model of storm-time atmospheric neutral density, published in Space Weather (2025) and released as an open, installable Python package with a worked example notebook."
collection: portfolio
order: 1
featured: true
image: "/images/portfolio/mltdm.png"
header:
  teaser: "portfolio/mltdm.png"
tags_list: ["Random forests", "scikit-learn", "Feature engineering", "Space Weather journal"]
links:
  - label: "Paper"
    url: "https://doi.org/10.1029/2024SW003928"
  - label: "GitHub"
    url: "https://github.com/kylermurphy/mltdm"
  - label: "Zenodo"
    url: "https://doi.org/10.5281/zenodo.15091438"
---

<img src="/images/portfolio/mltdm.png" alt="MLTDM: Machine-learning thermospheric density model" style="max-width:100%; border-radius:6px; margin-bottom:1em;">

Satellite drag in low-Earth orbit is driven by thermospheric neutral density, and density can change dramatically during geomagnetic storms. Empirical models often miss these storm-time changes, which matters for conjunction assessment and orbit prediction for LEO constellations.

**What I did**

- Built a random-forest regression model of neutral density trained on CHAMP and GRACE accelerometer-derived density, using solar EUV irradiance (FISM2) and solar-wind/geomagnetic (OMNI) drivers as features. Storm-time density can rise by up to a factor of ~10 over quiet levels; models combining solar and geomagnetic drivers performed best during storms.
- Used the model to unpack *why* density changes during storms: permutation feature importance and storm-phase analysis separate the solar and geomagnetic contributions to the density response.
- Packaged the model so others can use it: `pip install`, a config file, automatic download of the trained model and feature data, and an [example notebook](https://github.com/kylermurphy/mltdm/blob/main/Notebooks/RF_predict.ipynb) that produces global density maps like the one above.

**Outcome:** Peer-reviewed paper in *Space Weather* ([Murphy et al., 2025](https://doi.org/10.1029/2024SW003928)), with the model archived on [Zenodo](https://doi.org/10.5281/zenodo.15091438).

[Paper](https://doi.org/10.1029/2024SW003928) · [GitHub](https://github.com/kylermurphy/mltdm) · [Zenodo](https://doi.org/10.5281/zenodo.15091438)
