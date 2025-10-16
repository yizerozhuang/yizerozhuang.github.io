---
layout: default
title: Photos
---


# Photos

<div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(240px,1fr));gap:16px;">
{% for album in site.data.gallery.albums %}
  <a href="{{ '/gallery/' | append: album.slug | append: '/' | relative_url }}" style="text-decoration:none;color:inherit;">
    <figure style="margin:0;border:1px solid #444;background:#111;">
      <img src="{{ album.cover }}" alt="{{ album.title }} cover" style="width:100%;height:180px;object-fit:cover;display:block;"/>
      <figcaption style="padding:8px 10px;font-weight:bold;text-align:center;">{{ album.title }}</figcaption>
    </figure>
  </a>
{% endfor %}
</div>
