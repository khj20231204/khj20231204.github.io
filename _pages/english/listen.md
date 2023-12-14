---
title: "듣기"
layout: archive
permalink: /listen
author_profile: true
types: posts
sidebar:
  nav: "sidebar_category_list"
---

{% assign posts = site.categories['LISTEN']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}

