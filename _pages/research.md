---
layout: page
title: research
permalink: /research/
description: My work, grouped by the methods behind it.
nav: true
nav_order: 4
_styles: >
  .research-theme { margin-top: 2.4rem; }
  .research-theme:first-of-type { margin-top: 1rem; }
  .research-theme h2 { font-size: 1.5rem; font-weight: 400; margin-bottom: 0.3rem; padding-bottom: 0.35rem; border-bottom: 1px solid var(--global-divider-color); }
  .research-theme h2 a { color: inherit; }
  .research-theme h2 a:hover { color: var(--global-theme-color); text-decoration: none; }
  .research-theme .theme-intro { color: var(--global-text-color-light); margin: 0.6rem 0 1.1rem; }
  .research-theme .col { padding-bottom: 1.4rem; }
  .research-card, .research-card:hover { display: block; height: 100%; color: inherit; text-decoration: none; }
  .research-card .card { overflow: hidden; }
  .research-thumb { aspect-ratio: 16 / 9; background: #fff; display: flex; align-items: center; justify-content: center; overflow: hidden; }
  .research-thumb img { width: 100%; height: 100%; object-fit: contain; }
  .research-thumb.cover img, .research-thumb.themed img { object-fit: cover; }
  .research-thumb.placeholder { background: rgba(127, 127, 127, 0.08); }
  .research-thumb .research-icon { font-size: 2.6rem; color: var(--global-theme-color); opacity: 0.75; }
  html[data-theme="dark"] .research-thumb.themed { background: #212529; }
  .research-card .card-body { padding: 0.9rem 1.05rem 1.15rem; }
  .research-venue { font-size: 0.74rem; letter-spacing: 0.04em; text-transform: uppercase; color: var(--global-text-color-light); margin-bottom: 0.35rem; }
  .research-venue i { font-size: 0.65rem; margin-left: 0.15rem; }
  .research-card .card-title { font-size: 1.12rem; font-weight: 500; line-height: 1.3; margin-bottom: 0.45rem; }
  .research-card:hover .card-title { color: var(--global-theme-color); }
  .research-card .card-text { font-size: 0.88rem; margin-bottom: 0; }
---

{% for theme in site.data.research_themes %}
{% assign items = site.projects | where: "category", theme.key | sort: "importance" %}
{% if items.size > 0 %}

<section class="research-theme" id="{{ theme.key | slugify }}">
  <h2><a href="#{{ theme.key | slugify }}">{{ theme.title }}</a></h2>
  <p class="theme-intro">{{ theme.intro }}</p>
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in items %}
      {% include research_card.liquid %}
    {% endfor %}
  </div>
</section>
{% endif %}
{% endfor %}
