---
layout: default
title: Home
---
<center><h2>Cars and other obsesions.</h2>
<p>
Work hard and make mistakes, eventually it'll all work out! Through a mild amount of trial and error, I've come to own a mildly successful project car—my lil <a href="https://sudoyashi.com/dacabby">cabby</a>. I hate that car, but I love that car.
<br><br>

</center>

<hr>
<br>
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