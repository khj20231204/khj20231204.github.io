---
title: "SPRING_MASTER"
layout: archive
permalink: /spring_master
author_profile: true
types: posts
sidebar:
  nav: "sidebar_category_list"
---

{% assign posts = site.categories['SPRING_MASTER']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}

