---
layout: default
title: Home
---
<center><h2>Cars and other obsesions.</h2>
<p>
A home for all of my hobbies that I end up writing notes about. This includes my project cars, IT administration, cooking, and whatever other hobbies I'm working on. Most people might be here for my <a href="https://sudoyashi.com/dacabby">cabby</a>. But explore around, maybe you'll find something cool!
<br><br>
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