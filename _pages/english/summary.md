---
title: "요약"
layout: archive
permalink: /summary
author_profile: true
types: posts
sidebar:
  nav: "sidebar_category_list"
---

{% assign posts = site.categories['SUMMARY']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}

