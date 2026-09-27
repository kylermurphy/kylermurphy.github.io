---
permalink: /
title: "Kyle Murphy: space weather, machine learning, scientific software"
hide_title: true
excerpt: "Space weather scientist and independent consultant building machine-learning models, open-source tools, and research programs for satellite drag, orbit prediction, and space-weather risk."
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

{% include base_path %}

<section class="hero">
  <p class="hero__kicker">Space weather · Machine learning · Scientific software</p>
  <h1 class="hero__title">I build models that predict how space weather affects satellites and the systems we rely on.</h1>
  <p class="hero__lede">I'm Kyle Murphy, a space physicist and independent consultant in Thunder Bay, Ontario. I've spent 20+ years studying how geomagnetic storms reshape near-Earth space, at the University of Alberta and NASA Goddard. Today I turn that expertise into <strong>machine-learning models, open-source software, and research programs</strong> for teams working on satellite drag, orbit prediction, and space-weather risk.</p>
  <a class="btn btn--light" href="{{ base_path }}/portfolio/">See my work</a>
  <a class="btn btn--ghost" href="{{ base_path }}/cv/">CV / résumé</a>
  <a class="btn btn--ghost" href="mailto:{{ site.author.email }}">Get in touch</a>
</section>

<div class="stats">
  <div class="stats__item"><span class="stats__num">100+</span><span class="stats__label">peer-reviewed publications</span></div>
  <div class="stats__item"><span class="stats__num">20+</span><span class="stats__label">years in space physics research</span></div>
  <div class="stats__item"><span class="stats__num">5</span><span class="stats__label">open-source Python packages</span></div>
  <div class="stats__item"><span class="stats__num">NASA</span><span class="stats__label">Early Career Public Achievement Medal</span></div>
</div>

<h2 class="section-title">What I do</h2>

<div class="skills-grid">
  <div class="skill-card">
    <h3><i class="fa-solid fa-satellite" aria-hidden="true"></i>Space weather &amp; atmospheric density</h3>
    <p>Storm-time thermospheric density and satellite drag for LEO constellations, density derived from satellite orbits, radiation-belt dynamics, and ground-induced electric fields.</p>
  </div>
  <div class="skill-card">
    <h3><i class="fa-solid fa-chart-line" aria-hidden="true"></i>Machine learning &amp; statistics</h3>
    <p>Random forests and gradient boosting, time-series forecasting from solar and geomagnetic drivers, physics-informed feature engineering, storm-aware validation, and ensemble uncertainty.</p>
  </div>
  <div class="skill-card">
    <h3><i class="fa-solid fa-code" aria-hidden="true"></i>Scientific software &amp; data pipelines</h3>
    <p>Turning research code into installable, documented, tested Python packages. Multi-mission data ingestion, vectorization and parallel speed-ups, reproducible notebooks.</p>
  </div>
  <div class="skill-card">
    <h3><i class="fa-solid fa-people-group" aria-hidden="true"></i>Research leadership &amp; communication</h3>
    <p>Project management, proposal development, mission-concept studies, teaching scientific programming, and building community through an international seminar series.</p>
  </div>
</div>

<h2 class="section-title">Featured work</h2>

{% assign featured = site.portfolio | where: "featured", true | sort: "order" %}
<div class="card-grid">
{% for post in featured %}
  {% include kyle-card.html item=post %}
{% endfor %}
</div>
<p><a href="{{ base_path }}/portfolio/">See all projects &rarr;</a></p>

<h2 class="section-title">Latest notes</h2>
<ul class="recent-notes">
{% for post in site.posts limit:4 %}
  <li><time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %Y" }}</time> <a href="{{ base_path }}{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
</ul>
<p><a href="{{ base_path }}/notes/">All notes &rarr;</a></p>

<h2 class="section-title">Work with me</h2>

I work with research groups, agencies, and companies on:

- **Density and drag modelling:** building, validating, or benchmarking thermospheric density models (empirical, ML, or orbit-derived) for storm conditions.
- **Machine learning for space weather:** designing forecasting pipelines, choosing features and validation that respect storm physics, and reviewing existing models.
- **Research software:** turning notebooks and scripts into maintainable packages with tests, docs, and CI.
- **Proposals and science writing:** proposal development, mission science cases, and peer-reviewed papers.

The quickest way to reach me is [email](mailto:{{ site.author.email }}).
