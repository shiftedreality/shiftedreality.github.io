---
layout: page
permalink: /it-ai/
title: IT & AI
---

<div id="archives">
{% assign posts = site.categories['it-ai'] %}
{% if posts %}
  {% for post in posts %}
  <article class="archive-item">
    <h4><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h4>
    <p class="post_date">{{ post.date | date: "%B %e, %Y" }}</p>
  </article>
  {% endfor %}
{% else %}
  <p>No posts yet.</p>
{% endif %}
</div>
