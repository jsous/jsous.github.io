---
layout: page
title: Blog Posts
permalink: /blog-posts/
---

<ul class="post-list">
{% for post in site.posts %}
  <li class="post-list__item">
    <time class="post-list__date" datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %-d, %Y" }}</time>
    <div class="post-list__body">
      <h2 class="post-list__title"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
      {% if post.subtitle %}<p class="post-list__subtitle">{{ post.subtitle }}</p>{% endif %}
    </div>
  </li>
{% endfor %}
</ul>
