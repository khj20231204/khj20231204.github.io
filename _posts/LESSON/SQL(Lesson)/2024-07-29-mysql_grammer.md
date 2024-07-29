---
layout: single
title: 07_26.MySql설치
categories: SQL(Lesson)
tag: []
author_profile: false
---

1. # MySql과 오라클의 다른 점 
   create sequence -> auto_increment
   varchar2 -> varchar
   sysdate -> sysdate()

1. # 연산자

   정렬
   ```cs
      select * from boardtest order by no asc;  //1,2,3,...
      select * from boardtest order by no desc; //10,9,8,...
   ```

   limit : 추출할 데이터의 인덱스 번호, 추출할 데이터 갯수
   ```cs
      ex)select * from board order by no desc limit 0, 5; //최근 항목 5개 검색
   ```   


