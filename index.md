---
layout: page
title: Trang chủ
permalink: /
---

# 👋 Xin chào, mình là Nguyễn Phúc Ngọc Thành

Đây là nơi mình chia sẻ kiến thức về lập trình (Java, Spring Boot, React ...), kinh nghiệm thực tế và những gì mình học được trong hành trình phát triển phần mềm.

---

## 📝 Bài viết mới nhất

<ul class="post-list">
  {% for post in site.posts limit:5 %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <small>{{ post.date | date: "%d-%m-%Y" }}</small>
    </li>
  {% endfor %}
</ul>

<p><a href="/posts/">📚 Xem tất cả bài viết →</a></p>
