---
layout: default
title: Home
---
<center><h2>The pursuit of performance on a budget</h2>
<p>
This is my website, dedicated to a life of projects and wonder. And this is my car, a <a href="https://sudoyashi.com/dacabby">Volkswagen Golf Cabriolet Mk1</a>.
<br>
<br>
</center>
<hr><br>
<h2>Read something!</h2>

{% for post in paginator.posts %}
  {% include featured-post.html %}
{% endfor %}

<!-- Pagination links -->
<div class="pagination">
  {% if paginator.next_page %}
    <a class="pagination-button pagination-active next" href="{{ site.github.url }}{{ paginator.next_page_path }}">{{ site.data.settings.pagination.previous_page }}</a>
  {% else %}
    <span class="pagination-button">{{ site.data.settings.pagination.previous_page }}</span>
  {% endif %}
  {% if paginator.previous_page %}
    <a class="pagination-button pagination-active" href="{{ site.baseurl }}{{ paginator.previous_page_path }}">{{ site.data.settings.pagination.next_page }}</a>
  {% else %}
    <span class="pagination-button">{{ site.data.settings.pagination.next_page }}</span>
  {% endif %}
</div>