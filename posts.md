---
layout: page
title: Bài viết
permalink: /posts/
---

<ul class="post-list">
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <small>{{ post.date | date: "%d-%m-%Y" }}</small>
    </li>
  {% endfor %}
</ul>
