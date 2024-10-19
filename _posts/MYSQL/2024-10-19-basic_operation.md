---
layout: single
title: limit, offset에서 사칙연산
categories: MYSQL
tag: []
author_profile: false
---
 
1. # 사칙연산 지원 안됨

   limit와 offest에서 사칙연산은 지원되지 않습니다.   
   *mysql  Ver 8.0.39

   ```sql
      select 5+6; -- 11
      select * from board limit 10 offset 10+3; -- error발생
      select * from board limit (10+3) offset 3;   -- error발생
   ```

   자바에서 연산을 처리 후 마지막으로 하나의 값으로만 전달.