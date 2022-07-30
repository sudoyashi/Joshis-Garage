---
layout: page
title: Cars
permalink: /cars/
image: cars.jpg
tags: cars, audi, volkswagen, vag
---

<div id="car-archives">
{% for category in site.categories %}
  <div class="car-archive-group">
    {% capture category_name %}{{ category | first }}{% endcapture %}
    <div id="#{{ category_name | slugize }}"></div>
    <p></p>

    <h3 class="category-head">{{ category_name }}</h3>
    <a name="{{ category_name | slugize }}"></a>
    {% for post in site.categories[category_name] %}
    <article class="archive-item">
      <h4><a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a></h4>
    </article>
    {% endfor %}
  </div>
{% endfor %}
</div>

# 1985 Volkswagen Golf Cabriolet
![Cabby](assets/img/driveway1.jpg)
![Interior Cabby](assets/img/cabbyinterior-1.jpg)
![Cabby rear](assets/img/cabby-rear-1.jpg)
![Wheel](assets/img/cabby-gallery-7.jpg)
