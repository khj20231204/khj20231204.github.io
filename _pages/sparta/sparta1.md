---
title: "SPARTA1"
layout: archive
permalink: /sparta1
author_profile: true
types: posts
sidebar:
  nav: "sidebar_category_list"
---

{% assign posts = site.categories['SPARTA1']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}

