---
title: "단어"
layout: archive
permalink: /word
author_profile: true
types: posts
sidebar:
  nav: "sidebar_category_list"
---

{% assign posts = site.categories['WORD']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}

