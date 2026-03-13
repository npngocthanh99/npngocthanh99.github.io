---
layout: page
title: Home
permalink: /
---

# 👋 Hi, I'm Nguyen Phuc Ngoc Thanh

Welcome to my blog. This is where I share my journey in software development — including what I learn, the technologies I work with, and practical experiences from building real-world applications.

My main areas of interest include Java, Spring Boot, React, and backend system design.

---

## 📝 Latest Posts

<ul class="post-list">
  {% for post in site.posts limit:10 %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <small>{{ post.date | date: "%d-%m-%Y" }}</small>
    </li>
  {% endfor %}
</ul>

<p>
  <a href="/posts/">View all posts →</a>
</p>
