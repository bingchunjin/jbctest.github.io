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
    
    {% if category_parts.size == 2 %}
      <!-- 一级分类 A -->
      {% assign a_category = category_parts[0] %}
      {% assign b_category = category_parts[1] %}

      {% comment %}
        Ensure that the A-B structure exists before rendering
      {% endcomment %}
      
        <h3>{{ a_category }}</h3>
        {% assign subcategories = site.categories[a_category+'/'+b_category] | default: empty_array %}
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
      
    {% endif %}
  {% endfor %}

</section>
<!-- /section.content -->
