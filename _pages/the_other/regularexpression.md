---
title: "RegularExpression"
layout: archive
permalink: /regularexpression
author_profile: true
types: posts
sidebar:
  nav: "sidebar_category_list"
---

{% assign posts = site.categories['RegularExpression']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}

