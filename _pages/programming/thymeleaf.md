---
title: "Thymeleaf"
layout: archive
permalink: /thymeleaf
author_profile: true
types: posts
sidebar:
  nav: "sidebar_category_list"
---

{% assign posts = site.categories['Thymeleaf']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}