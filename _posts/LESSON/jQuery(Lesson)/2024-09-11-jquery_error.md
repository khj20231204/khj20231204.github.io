---
layout: single
title: jQuery 에러
categories: jQuery(Lesson)
tag: []
author_profile: false
---

1. script 부분
   ```js
      //error 발생
      <script src="http://code.jquery.com/jquery-latest.js" /> 

      //정상 작동
      <script src="http://code.jquery.com/jquery-latest.js"></script>
   ```   
    jQuery 주소를 추가할 때 마지막 닫는 태그를 `/>` 이렇게 닫으면 제대로 동작하지 않음.   
    반드시 `</script>` 이렇게 닫아야 됨.    