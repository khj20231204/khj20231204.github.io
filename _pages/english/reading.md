---
title: "독해"
layout: archive
permalink: /reading
author_profile: true
types: posts
sidebar:
  nav: "sidebar_category_list"
---

{% assign posts = site.categories['READING']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}

