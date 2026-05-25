---
layout: default
title: 首页
---

<div class="home-intro">
  <h1>欢迎来到我的学习博客</h1>
  <p>这里记录着我的学习历程、技术心得和课程实验成果。通过分享知识，不断提升自己，也希望能帮助到更多志同道合的学习者。</p>
</div>

<h2>最近文章</h2>
<div class="posts-list">
  {% for post in site.posts %}
  <article class="post-item">
    <h3><a href="{{ post.url | relative_url }}" class="post-title">{{ post.title }}</a></h3>
    <div class="post-meta">
      <span>{{ post.date | date: "%Y年%m月%d日" }}</span>
      <span>分类：{{ post.category }}</span>
    </div>
    <p class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
  </article>
  {% endfor %}
</div>