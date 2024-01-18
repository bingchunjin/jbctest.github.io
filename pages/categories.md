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
  {{ site.categories | inspect }}
  {% for category in sorted_categories %}
    {% assign category_parts = category | first | split: '/' %}

    {% if category_parts.size == 1 %}
      <!-- 一级分类 -->
      <h3>{{ category_parts[0] }}</h3>
      {% assign subcategories = site.categories[category_parts[0] + '/' + category_parts[1]] %}
      {{ subcategories.size | inspect }}
      {% if subcategories.size > 0 %}
        {% for subcategory in subcategories %}
         {{ subcategory | inspect }}
          {% assign subcategory_parts = subcategory | first | split: '/' %}
          <h4>{{ subcategory_parts[1] }}</h4>
          <ol class="posts-list">
            {% for post in subcategory.last %}
              <li class="posts-list-item">
                <span class="posts-list-meta">{{ post.date | date:"%Y-%m-%d" }}</span>
                <a class="posts-list-name" href="{{ site.url }}{{ post.url }}">{{ post.title }}</a>
              </li>
            {% endfor %}
          </ol>
        {% endfor %}
      {% endif %}
    {% endif %}
  {% endfor %}

</section>
<!-- /section.content -->
