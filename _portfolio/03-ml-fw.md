---
title: "ml_fw: an ML toolkit for space-weather forecasting"
kicker: "Machine learning · Uncertainty"
excerpt: "Reusable building blocks for time-series ML in heliophysics: lagged features, tuning, diagnostics, and ARIMA-based perturbed-input ensembles for forecast uncertainty."
collection: portfolio
order: 3
featured: true
image: "/images/portfolio/ml_fw.png"
header:
  teaser: "portfolio/ml_fw.png"
tags_list: ["pandas", "scikit-learn", "statsmodels", "ARIMA ensembles"]
links:
  - label: "GitHub"
    url: "https://github.com/kylermurphy/ml_fw"
---

<img src="/images/portfolio/ml_fw.png" alt="ml_fw: an ML toolkit for space-weather forecasting" style="max-width:100%; border-radius:6px; margin-bottom:1em;">

`ml_fw` packages the workflow I use again and again when building forecasting models from solar-wind and geomagnetic data, so each new project starts from tested components rather than a blank notebook.

- **Feature preparation:** log transforms for wide-dynamic-range drivers, sin/cos encoding for periodic variables (local time, longitude), and time-lagged features.
- **Training and tuning:** a scikit-learn wrapper with (optionally subsampled) grid search and multi-metric parameter selection.
- **Diagnostics:** correlation profiling, binned and rolling error metrics, and plotting for residuals by driver or storm phase.
- **Uncertainty:** an ARIMA-residual *perturbed-input ensemble* that generates realistic noisy versions of the model inputs (figure above) to show how input uncertainty propagates to the forecast.

[GitHub](https://github.com/kylermurphy/ml_fw)
