---
layout: categories
title: Categories
description: 哈哈，你找到了我的文章基因库
keywords: 分类
comments: false
menu: 分类
permalink: /categories/
---

<section class="container posts-content">
  {% assign sorted_categories = site.categories | sort %}
  {% for category in sorted_categories %}
    {% assign category_name_parts = category | first | split: '/' %}

    {% if category_name_parts.size == 1 %}
      <!-- 一级分类 -->
      <h3 id="{{ category_name_parts[0] }}">{{ category_name_parts[0] }}</h3>
      <ol class="posts-list">
    {% else %}
      <!-- 二级分类 -->
      {% unless forloop.first %}
        </ol>
      {% endunless %}
      <h4 id="{{ category_name_parts[1] }}">{{ category_name_parts[1] }}</h4>
      <ol class="posts-list">
    {% endif %}

    {% for post in category.last %}
      <li class="posts-list-item">
        <span class="posts-list-meta">{{ post.date | date:"%Y-%m-%d" }}</span>
        <a class="posts-list-name" href="{{ site.url }}{{ post.url }}">{{ post.title }}</a>
      </li>
    {% endfor %}

    {% if forloop.last %}
      </ol>
    {% endif %}
  {% endfor %}
</section>

<!-- /section.content -->
