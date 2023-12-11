---
title: "SQL"
layout: archive
permalink: /sql
author_profile: true
types: posts
---

{% assign posts = site.categories['SQL']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}

<!-- 
posts = site.categories['a'] 
posts의 categories가 a 인걸 for문을 돌면서 묶는다

permalink는 고정된 static한 링크다. 
navigation.yml의 url: /a_categories/sql_permalink
을 클릭하면 여기로 링크가 되고 여기 md파일에 할당된
permalink에 의해 이 페이지가 실행된다

site.
-->