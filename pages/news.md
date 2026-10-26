---
layout: page
title: News
permalink: /news/
---

{% assign items = site.data.news | sort: "date" | reverse %}
{% assign current_year = "" %}
{% assign has_tweet = false %}
{% for item in items %}
{% unless item.show == false %}
{% assign year = item.date | date: "%Y" %}
{% if year != current_year %}
{% unless current_year == "" %}</ul>{% endunless %}
<h2 class="news-year">{{ year }}</h2>
<ul class="news-list">
{% assign current_year = year %}
{% endif %}
  <li class="news-item">
    <span class="news-date">{{ item.date | date: "%B %Y" }}</span>
    <div class="news-body">
      {{ item.text | markdownify }}
      {% if item.tweet %}
      {% assign has_tweet = true %}
      <blockquote class="twitter-tweet" data-dnt="true"><a href="{{ item.tweet }}">Post on X</a></blockquote>
      {% endif %}
      {% if item.tweets %}
      {% assign has_tweet = true %}
      <div class="news-tweets">
      {% for t in item.tweets %}
      {% if t.url %}{% assign t_url = t.url %}{% else %}{% assign t_url = t %}{% endif %}
      <div class="news-tweet">
        {% if t.label %}<p class="news-tweet-label">{{ t.label }}</p>{% endif %}
        <blockquote class="twitter-tweet" data-dnt="true"><a href="{{ t_url }}">Post on X</a></blockquote>
      </div>
      {% endfor %}
      </div>
      {% endif %}
    </div>
  </li>
{% endunless %}
{% endfor %}
{% unless current_year == "" %}</ul>{% endunless %}

{% if has_tweet %}
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
{% endif %}
