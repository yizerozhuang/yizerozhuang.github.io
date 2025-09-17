---
layout: default
title: Photos
---

<nav>
  <a href="{{ '/' | relative_url }}">Home</a> ·
  <a href="{{ '/blog/' | relative_url }}">Blog</a> ·
  <a href="{{ '/photos/' | relative_url }}">Photos</a> ·
  <a href="{{ '/resume/' | relative_url }}">Resume</a>
  <hr />
</nav>

# Photos

<div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:16px;">
{% for photo in site.data.photos %}
  <figure>
    <img src="{{ photo.url }}" alt="{{ photo.title }}" style="width:100%;height:auto;border:1px solid #444;"/>
    <figcaption><strong>{{ photo.title }}</strong><br/>{{ photo.caption }}</figcaption>
  </figure>
{% endfor %}
</div>
