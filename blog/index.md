---
layout: default
title: Blog
---

<nav>
  <a href="{{ '/' | relative_url }}">Home</a> ·
  <a href="{{ '/blog/' | relative_url }}">Blog</a> ·
  <a href="{{ '/gallery/' | relative_url }}">Photos</a> ·
  <a href="{{ '/resume/' | relative_url }}">Resume</a>
  <hr />
</nav>

# Blog

{% if site.posts.size == 0 %}
<p>No posts yet. Create files in <code>_posts/</code> to get started.</p>
{% endif %}

<ul>
{% for post in site.posts %}
  <li>
    <span>{{ post.date | date: "%b %-d, %Y" }}</span> —
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
  </li>
{% endfor %}
  </ul>
