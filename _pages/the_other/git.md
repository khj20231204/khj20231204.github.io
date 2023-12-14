---
title: "Git"
layout: archive
permalink: /git
author_profile: true
types: posts
sidebar:
  nav: "sidebar_category_list"
---

{% assign posts = site.categories['Git']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}

