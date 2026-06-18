---
layout: page
permalink: /finance-investing/
title: Finance & Investing
---

<div id="archives">
{% assign posts = site.categories['finance-investing'] %}
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
