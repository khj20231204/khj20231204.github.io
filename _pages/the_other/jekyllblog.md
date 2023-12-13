---
title: "JekyllBlog"
layout: archive
permalink: /jekyllblog
author_profile: true
types: posts
sidebar:
  nav: "sidebar_category_list"
---

{% assign posts = site.categories['JekyllBlog']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}