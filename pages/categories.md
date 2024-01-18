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
  {% assign displayed_categories = "" %}
  {% for category in sorted_categories %}
    {% assign category_parts = category | first | split: '/' %}
    
    {% if category_parts.size == 2 %}
      {% assign main_category = category_parts[0] %}
      {% unless displayed_categories contains main_category %}
        <!-- 一级分类 A -->
        <h3>{{ main_category }}</h3>
        {% assign displayed_categories = displayed_categories | append: main_category | append: ";" %}
        {% assign subcategories = site.categories[main_category] %}
        {% if subcategories.size > 0 %}
          {% for subcategory in subcategories %}
            {% assign subcategory_parts = subcategory | first | split: '/' %}
            {% if subcategory_parts.size == 1 %}
              <!-- 二级分类 B -->
              <h4>{{ subcategory_parts[0] }}</h4>
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
      {% endunless %}
    {% endif %}
  {% endfor %}
</section>
<!-- /section.content -->
