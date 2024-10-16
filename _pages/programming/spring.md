---
title: "SPRING"
layout: archive
permalink: /spring
author_profile: true
types: posts
sidebar:
  nav: "sidebar_category_list"
---

{% assign posts = site.categories['SPRING']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}

