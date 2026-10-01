---
layout: page
permalink: /gallery/
title: gallery
description:
nav: true
nav_order: 2
---

<!-- Drop .jpg/.jpeg/.png/.webp files into assets/img/gallery/ and they appear here automatically, sorted by filename. -->

{% assign photos = site.static_files | where_exp: "f", "f.path contains '/assets/img/gallery/'" | sort: "path" %}
{% assign shown = 0 %}

<div class="row">
  {% for photo in photos %}
    {% assign ext = photo.extname | downcase %}
    {% assign size_suffix = photo.basename | split: '-' | last %}
    {% comment %} Skip the -480/-800/-1400 copies the responsive-image plugin generates. {% endcomment %}
    {% if size_suffix == '480' or size_suffix == '800' or size_suffix == '1400' %}{% continue %}{% endif %}
    {% if ext == '.jpg' or ext == '.jpeg' or ext == '.png' or ext == '.webp' %}
      {% assign shown = shown | plus: 1 %}
      <div class="col-sm-6 col-md-4 mb-4">
        {% include figure.liquid loading="lazy" path=photo.path class="img-fluid rounded" zoomable=true alt=photo.basename %}
      </div>
    {% endif %}
  {% endfor %}
</div>

{% if shown == 0 %}
🚧 under construction 🚧
<!-- <p>No photos yet. Add images to <code>assets/img/gallery/</code>.</p> -->
{% endif %}
