---
layout: base
title: "Tất Cả Bài Viết"
permalink: /posts/
---

<div class="post-hero">
  <div class="post-hero__inner">
    <span class="post-hero__tag tag--other">Archive</span>
    <h1 class="post-hero__title">Tất Cả Bài Viết</h1>
    <div class="post-hero__meta">
      <span class="post-hero__date">{{ site.posts | size }} bài viết</span>
    </div>
  </div>
</div>

<div class="l-main" style="grid-template-columns: 1fr;">
  <div>
    <div class="section-head">
      <h2 class="section-title">FULL <span>ARCHIVE</span></h2>
      <span class="section-count">{{ site.posts | size }} bài viết</span>
    </div>

    <div class="post-list">
      {% assign sorted = site.posts | sort: 'date' | reverse %}
      {% for post in sorted %}
        {% assign tag = post.tag | default: 'other' %}
        {% assign tag_label = 'Blog' %}
        {% if tag == 'java'   %}{% assign tag_label = 'Java'   %}{% endif %}
        {% if tag == 'spring' %}{% assign tag_label = 'Spring' %}{% endif %}
        {% if tag == 'react'  %}{% assign tag_label = 'React'  %}{% endif %}
        {% if tag == 'redis'  %}{% assign tag_label = 'Redis'  %}{% endif %}
        {% if tag == 'devops' %}{% assign tag_label = 'DevOps' %}{% endif %}
        {% if tag == 'cs'     %}{% assign tag_label = 'CS'     %}{% endif %}

        <a class="post-card reveal" href="{{ post.url | relative_url }}">
          <div class="post-card__num">{{ forloop.index | prepend: '0' | slice: -2, 2 }}</div>
          <div class="post-card__body">
            <span class="post-card__tag tag--{{ tag }}">{{ tag_label }}</span>
            <div class="post-card__title">{{ post.title }}</div>
            <div class="post-card__excerpt">{{ post.excerpt | strip_html | truncate: 130 }}</div>
          </div>
          <div class="post-card__meta">
            <div class="post-card__date">{{ post.date | date: "%d/%m/%Y" }}</div>
          </div>
        </a>
      {% endfor %}
    </div>

  </div>
</div>
