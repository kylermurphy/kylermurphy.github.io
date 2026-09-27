---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

<p class="cv-summary"><strong>Space weather scientist and machine-learning consultant</strong> with 20+ years of research experience across the University of Alberta, NASA Goddard Space Flight Center, and independent consulting. I combine deep domain knowledge of geomagnetic storms, the thermosphere, and the radiation belts with hands-on machine learning and software engineering. I deliver models, tools, and analyses that people can actually use: 100+ peer-reviewed papers, open-source Python packages, and a NASA Early Career Public Achievement Medal.</p>

<div class="cv-actions">
  <a class="btn btn--primary" href="mailto:{{ site.author.email }}">Contact me</a>
  <a class="btn btn--inverse" href="{{ base_path }}/portfolio/">Portfolio</a>
  <a class="btn btn--inverse" href="javascript:window.print()">Print / save as PDF</a>
</div>

## Core expertise

<table class="skill-table">
  <tr><td>Space weather</td><td>Storm-time thermospheric density and satellite drag; orbit-derived density (energy dissipation rate); radiation belts and ULF waves; substorms; ground magnetometers and geoelectric fields</td></tr>
  <tr><td>Machine learning &amp; statistics</td><td>Random forests, gradient boosting (XGBoost), hyperparameter optimization (Optuna, grid search), walk-forward and storm-aware cross-validation, feature importance, ARIMA-based ensembles, statistical and superposed-epoch analysis</td></tr>
  <tr><td>Software</td><td>Python (NumPy, pandas, scikit-learn, statsmodels, Dask), Jupyter, Git/GitHub, packaging, testing and CI; Orekit and SPICE for orbit and ephemeris work; Linux</td></tr>
  <tr><td>Data</td><td>Satellite accelerometer density (CHAMP, GRACE), precise orbits (SP3), OMNI solar wind, FISM2 solar EUV, ground magnetometer arrays (CARISMA, IMAGE, THEMIS)</td></tr>
  <tr><td>Leadership</td><td>Project management, proposal development, mission-concept science, teaching and mentoring, community seminar organization, science communication</td></tr>
</table>

## Experience

<div class="cv-job">
  <div class="cv-job__head"><h3 class="cv-job__role">Independent Consultant: Research Scientist, Data Analyst &amp; Project Manager</h3><span class="cv-job__dates">Feb 2021 – present</span></div>
  <p class="cv-job__org">Self-employed · Thunder Bay, Ontario</p>
  <ul>
    <li>Develop machine-learning models of storm-time thermospheric density for satellite-drag applications. Built a random-forest density model (<a href="https://doi.org/10.1029/2024SW003928">Space Weather, 2025</a>) released as the open-source <a href="https://github.com/kylermurphy/mltdm">MLTDM</a> package.</li>
    <li>Design gradient-boosted forecasting pipelines with per-horizon Optuna tuning, sample weighting, storm-aware walk-forward validation, and physically motivated features from Dst and F10.7.</li>
    <li>Built <a href="https://github.com/kylermurphy/contigo_edr">CONTIGO</a>, a modular framework that derives effective atmospheric density from spacecraft and constellation orbits, validated against Orekit.</li>
    <li>Built <a href="https://github.com/kylermurphy/ml_fw">ml_fw</a>, a reusable ML toolkit for space-weather time series (lagged features, tuning, diagnostics, perturbed-input ensembles for uncertainty).</li>
    <li>Sped up JB2008 density predictions by ~11x through vectorization and parallelization, enabling large statistical and ML studies.</li>
    <li>Lead author of the target and science-visibility study for the STORM global-imaging mission concept (<a href="https://doi.org/10.3389/fspas.2024.1394655">2024</a>). Provide research analysis, project management, and proposal development for clients.</li>
  </ul>
</div>

<div class="cv-job">
  <div class="cv-job__head"><h3 class="cv-job__role">Assistant Researcher</h3><span class="cv-job__dates">2017 – 2021</span></div>
  <p class="cv-job__org">Department of Astronomy, University of Maryland · contractor at NASA Goddard Space Flight Center</p>
  <ul>
    <li>Led research on radiation-belt electron loss and acceleration, ULF waves, and substorm dynamics using multi-mission satellite and ground-based data.</li>
    <li>Taught <em>Introduction to Astrophysical Programming</em> (Unix, Python, numerical methods, visualization, Git/GitHub).</li>
    <li>Received the NASA Early Career Public Achievement Medal (2020) and a NASA Heliophysics Science Division Peer Award (2020).</li>
  </ul>
</div>

<div class="cv-job">
  <div class="cv-job__head"><h3 class="cv-job__role">Researcher</h3><span class="cv-job__dates">2016 – 2017</span></div>
  <p class="cv-job__org">Universities Space Research Association</p>
</div>

<div class="cv-job">
  <div class="cv-job__head"><h3 class="cv-job__role">NSERC Postdoctoral Fellow</h3><span class="cv-job__dates">2014 – 2016</span></div>
  <p class="cv-job__org">NASA Goddard Space Flight Center</p>
  <ul>
    <li>Independent research program on the global response of the outer radiation belt during geomagnetic storms. NASA Heliophysics Science Division Peer Award (2015).</li>
  </ul>
</div>

<div class="cv-job">
  <div class="cv-job__head"><h3 class="cv-job__role">Research Assistant &amp; Teaching Assistant</h3><span class="cv-job__dates">2005 – 2014</span></div>
  <p class="cv-job__org">Department of Physics, University of Alberta</p>
  <ul>
    <li>Ph.D. and M.Sc. research on ULF waves and substorm onset using ground magnetometer and all-sky imager networks. Developed automated detection methods for auroral breakup.</li>
    <li>Taught first- and second-year physics labs of up to 60 students, including weekly lectures on scientific analysis, reporting, and computation.</li>
  </ul>
</div>

## Education

- **Ph.D., Physics**, University of Alberta, 2013
- **M.Sc., Physics**, University of Alberta, 2009
- **B.Sc., Specialization in Astrophysics**, University of Alberta, 2007 (First Class Standing)

## Selected awards

- NASA Early Career Public Achievement Medal (2020)
- NASA Heliophysics Science Division Peer Award (2020, 2015)
- NSERC Postdoctoral Fellowship (2014)
- Excellence in Science and Technology Public Awareness award (2013)
- NSERC graduate scholarships: Doctoral (2009) and Master's (2007)
- President's Doctoral Prize of Distinction (2009)

<details>
<summary>All awards and scholarships</summary>
<ul>
<li>NASA Early Career Public Achievement Medal, 2020</li>
<li>NASA Heliophysics Science Division Peer Award, 2020</li>
<li>NASA Heliophysics Science Division Peer Award, 2015</li>
<li>NSERC Postdoctoral Fellowship, 2014</li>
<li>Excellence in Science and Technology Public Awareness, 2013</li>
<li>Dissertation Fellowship, 2013</li>
<li>Andrew Stewart Memorial Graduate Prize, 2012</li>
<li>Alberta Innovates, 2011</li>
<li>Natural Sciences and Engineering Research Council (NSERC) Graduate Scholarship, Doctoral, 2009</li>
<li>Alberta Ingenuity, 2009</li>
<li>President's Doctoral Prize of Distinction, 2009</li>
<li>NSERC Canada Graduate Scholarship, Master's, 2007</li>
<li>Queen Elizabeth II Graduate Scholarship, 2007</li>
<li>Department of Physics Entrance Scholarship, 2007</li>
<li>Walter H. Johns Graduate Scholarship, 2007</li>
<li>J. A. Jacobs Prize in Physics, 2007</li>
<li>Vega Prize for Astronomy, 2006</li>
<li>Douglas M. Sheppard Memorial Scholarship, 2003</li>
<li>Academic Excellence Scholarship, 2002</li>
</ul>
</details>

## Teaching

- **Introduction to Astrophysical Programming** (University of Maryland): Unix and the shell, scientific Python, good programming style, numerical methods, visualization, and version control with Git/GitHub.
- **First- and second-year physics labs** (University of Alberta): labs of up to 60 students; developed weekly lectures on scientific analysis, reporting, and computational analysis.

## Service & community

- [Magnetosphere Online Seminar Series](https://msolss.github.io/MagSeminars/): international seminar series on Zoom and YouTube, started during COVID-19 to keep the space physics community connected.
- Open-source maintainer: [GMAG](https://github.com/kylermurphy/gmag), [MLTDM](https://github.com/kylermurphy/mltdm), [CONTIGO](https://github.com/kylermurphy/contigo_edr), [ml_fw](https://github.com/kylermurphy/ml_fw).

## Selected publications

{% assign selected = "2025-01-06-Murphy,2024-09-26-Murphy,2023-07-19-Murphy,2022-11-04-Murphy,2016-10-01-Mann,2018-05-01-Ozeke,2018-11-01-Kalmoni" | split: "," %}
<ol>{% for post in site.publications reversed %}{% assign fname = post.path | split: '/' | last | remove: '.md' %}{% if selected contains fname %}
  {% include archive-single-cv-pub.html %}
{% endif %}{% endfor %}</ol>

<details>
<summary>Full publication list ({{ site.publications | size }} papers)</summary>
<ol>{% for post in site.publications reversed %}
  {% include archive-single-cv-pub.html %}
{% endfor %}</ol>
</details>

Also on [Google Scholar]({{ site.author.googlescholar }}).
