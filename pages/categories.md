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
  {% for a_category in sorted_categories %}
    {% assign a_category_parts = a_category | first | split: '/' %}
     {{ a_category_parts.size | inspect }}
    {% if a_category_parts.size == 2 %}
      <!-- 一级分类 A -->
      <h3>{{ a_category_parts[0] }}</h3>

      {% assign a_subcategories = site.categories[a_category_parts[0]] | default: empty_array %}
      {% if a_subcategories.size > 0 %}
        {% for b_category in a_subcategories %}
          {% assign b_category_parts = b_category | first | split: '/' %}
          {% if b_category_parts.size == 1 %}
            <!-- 二级分类 B -->
            <h4>{{ b_category_parts[0] }}</h4>
            <ol class="posts-list">
              {% for post in b_category.last %}
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
