---
permalink: /blog/
title: "Notes"
excerpt: "All research notes"
author_profile: true
---

<span class='anchor' id='blog-list'></span>

# <i class="fas fa-blog"></i> All Notes

<div class="blog-grid">
{% assign english_posts = site.posts | where: "lang", "en" %}
{% assign legacy_posts = site.posts | where_exp: "post", "post.lang == null" %}
{% assign sorted_posts = english_posts | concat: legacy_posts | sort: 'date' | reverse %}
{% for post in sorted_posts %}
  <div class="blog-card">
    <a href="{{ post.url | relative_url }}" class="blog-card-link">
      <div class="blog-card-image">
        <div class="blog-badge">{{ post.date | date: "%B, %Y" }}</div>
        {% if post.cover_image %}
        <img src="{{ post.cover_image | relative_url }}" alt="{{ post.title }}">
        {% else %}
        <img src="{{ '/images/default-blog-cover.svg' | relative_url }}" alt="{{ post.title }}">
        {% endif %}
      </div>
    </a>
      <div class="blog-card-content">
        <a href="{{ post.url | relative_url }}" class="blog-card-link">
          <div class="blog-title">{{ post.title }}</div>
        </a>
        <div class="blog-description">{{ post.description | default: post.excerpt | strip_html | truncate: 150 }}</div>
        {% if post.translation_key %}
          {% assign zh_versions = site.posts | where: "translation_key", post.translation_key | where: "lang", "zh" %}
          {% assign zh_post = zh_versions | first %}
          {% if zh_post %}
        <div class="blog-language-links">
          <a href="{{ zh_post.url | relative_url }}"><i class="fas fa-language"></i> 中文版本</a>
        </div>
          {% endif %}
        {% endif %}
      </div>
  </div>
{% endfor %}
</div>

{% if site.posts.size == 0 %}
<div class="quote-accent">
  <p>No blog posts yet. Check back soon!</p>
</div>
{% endif %}
