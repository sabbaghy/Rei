---
layout: archive
permalink: /data-science/
title: "Data Science Posts by Category"
categories: [data-science]
author_profile: true
header:
    image: "/images/Austin.JPG"
---
{% for category in site.categories %}
  <h3>{{ category[0] }}</h3>
  <ul>
    {% for post in category[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}