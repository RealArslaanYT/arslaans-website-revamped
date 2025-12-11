---
layout: base
title: Blog
permalink: /blog/
nav_order: 2
---

<ul class="posts-list">
  {% for post in site.posts %}
    <li class="post">
    <a href="{{ post.url }}" class="white" style="text-decoration: none;">
      {% if post.image %}
        <img src="{{ post.image }}" alt="{{ post.title }}" class="post-image"/>
      {% endif %}

      <h1>{{ post.title }}</h1>
      <p class="post-meta">{{ post.date | date: "%B %-d, %Y" }} | {{ post.author }}</p>
      </a>
    </li>

{% endfor %}

</ul>
