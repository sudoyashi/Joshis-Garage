---
layout: default
title: Home
---
<img src="assets/img/driveway1.jpg" alt="1985 Golf Mk1 Convertible">
<br>


<center><h2> Refuse to Give Up </h2>
<p>
If there's anything that you really need to keep a project car is tenacity and money. Refuse to give up, but don't forget to eat once in a while.

Want to start a project car on your own?  <a href="/_posts/2022-01-03-firstprojectcar.markdown">Read here!</a> Otherwise, checkout my posts below.
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
