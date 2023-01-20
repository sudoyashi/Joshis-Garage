---
layout: page
title: Cars
permalink: /cars/
---
Test

## 1985 Volkswagen Golf Cabriolet
![Cabby](https://sudoyashi.github.io/Joshis-Garage/assets/img/driveway1.jpg)
![Interior Cabby](https://sudoyashi.github.io/Joshis-Garage/assets/img/cabbyinterior-1.jpg)
![Cabby rear](https://sudoyashi.github.io/Joshis-Garage/assets/img/cabby-rear-1.jpg)
![Wheel](https://sudoyashi.github.io/Joshis-Garage/assets/img/cabby-gallery-7.jpg)

## Cabby Links

1. [Bike Carb Conersion Guide](https://sudoyashi.github.io/Joshis-Garage/carbconversion)
2. [Carpet Replacement](https://sudoyashi.github.io/Joshis-Garage/carpet)

## 2019 Honda Civic Si

![Civic Front](https://sudoyashi.github.io/Joshis-Garage/assets/img/pages/cars/civic-full.jpg)
![Civic Front](https://sudoyashi.github.io/Joshis-Garage/assets/img/pages/cars/civic-rear.jpg)
![Civic Front](https://sudoyashi.github.io/Joshis-Garage/assets/img/pages/cars/civic-side.jpg)

## Civic Links


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

