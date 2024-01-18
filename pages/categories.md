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
    {% assign category_parts = category | first | split: '/' %}
    {{ category_parts.size | inspect }}
    {% if category_parts.size == 1 %}
      <!-- 一级分类 -->
      {% assign subcategories = site.categories[category_parts[0]] | default: empty_array %}
      {% if subcategories.size > 0 %}
        {% for subcategory in subcategories %}
          {% assign subcategory_parts = subcategory | first | split: '/' %}
          {% if subcategory_parts.size == 1 %}
            <!-- 二级分类 -->
            <h3>{{ subcategory_parts[0] }}</h3>
            <ol class="posts-list">
              {% for post in subcategory.last %}
                <li class="posts-list-item">
                  <span class="posts-list-meta">{{ post.date | date:"%Y-%m-%d" }}</span>
                  <a class="posts-list-name" href="{{ site.url }}{{ post.url }}">{{ post.title }}</a>
                </li>
              {% endfor %}
            </ol>
          {% endif %}
        {% endfor %}
      {% endif %}
    {% endif %}
  {% endfor %}
  
</section>
<!-- /section.content -->
