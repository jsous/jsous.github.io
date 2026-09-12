---
layout: page
title: Blog Posts
permalink: /blog-posts/
---

<div class="post-list">
  {% for post in site.posts %}
    <article class="post-list__item">
      <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %-d, %Y" }}</time>
      <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
      {% if post.subtitle %}<p>{{ post.subtitle }}</p>{% endif %}
    </article>
  {% endfor %}
</div>
