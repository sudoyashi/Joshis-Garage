---
layout: page
title: Posts
permalink: /posts/
---

# Posts

Find my (very) periodic posts here. Or something.

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>