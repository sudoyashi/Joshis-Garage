---
layout: default
title: Home
---
<center><h2>Cars and other obsesions.</h2>
<p>
My project car notes and other hobbies I'm working on. But while you're here, read about <a href="https://sudoyashi.github.io/Joshis-Garage/firstprojectcar">starting your own shitty project car!</a> <br><br>
Otherwise, checkout my posts below.
</p>


</center>

<hr>
<br>
<h2> Most recent posts...</h2>

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