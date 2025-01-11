---
title: "SPARTA2"
layout: archive
permalink: /sparta2
author_profile: true
types: posts
sidebar:
  nav: "sidebar_category_list"
---

{% assign posts = site.categories['SPARTA2']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}

