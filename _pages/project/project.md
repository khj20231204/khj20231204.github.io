---
title: "PROJECT"
layout: archive
permalink: /project
author_profile: true
types: posts
sidebar:
  nav: "sidebar_category_list"
---

{% assign posts = site.categories['PROJECT']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}

