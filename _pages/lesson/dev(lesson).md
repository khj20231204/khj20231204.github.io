---
title: "DEV(Lesson)"
layout: archive
permalink: /dev(lesson)
author_profile: true
types: posts
sidebar:
  nav: "sidebar_category_list"
---

{% assign posts = site.categories['DEV(Lesson)']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}

