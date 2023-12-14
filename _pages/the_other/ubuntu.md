---
title: "Ubuntu"
layout: archive
permalink: /ubuntu
author_profile: true
types: posts
sidebar:
  nav: "sidebar_category_list"
---

{% assign posts = site.categories['Ubuntu']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}

