---
layout: default
title: 文章分类
---

<div class="categories-page">
  <h1>文章分类</h1>

  {% assign categories = site.categories | sort %}
  {% for category in categories %}
  <div class="category-section" id="{{ category[0] | slugify }}">
    <h2>{{ category[0] }}</h2>
    <ul>
      {% for post in category[1] %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        <span>{{ post.date | date: "%Y-%m-%d" }}</span>
      </li>
      {% endfor %}
    </ul>
  </div>
  {% endfor %}
</div>