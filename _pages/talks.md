---
layout: archive
title: "Talks and presentations"
categories: [data-science]
permalink: /talks/
author_profile: true
header:
   image: "/images/Austin.jpg"
---
{% for category in site.categories %}
  <h3>{{ category[0] }}</h3>
  <ul>
    {% for post in category[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}