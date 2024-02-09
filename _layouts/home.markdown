---
layout: default
title: Home
---
![Homepage](https://www.sudoyashi.com/assets/img/cabby-gallery-5.jpg)
<center><h2>Unprofessional performance</h2>
<p>
A collection of unprofessional thoughts in racing, diy, IT, and other boy things. And home to my project car, the <a href="https://sudoyashi.com/dacabby">Volkswagen Golf Cabriolet MK1</a>.
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