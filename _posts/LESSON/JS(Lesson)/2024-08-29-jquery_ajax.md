---
layout: single
title: ajax
categories: jQuery(Lesson)
tag: []
author_profile: false
---

1. # Ajax란
   JavaScript와 XML을 이용한 비동기 통신처리를 구현하는 기술
   JavaScript로 웹 페이지 전체를 새로고침하지 않고, 일부 정보를 서버와 데이터를 주고 받는 경우에 사용한다.
   JavaScript를 이용해서 서버에서 데이터를 가져와 페이지 전체의 갱신(refresh)없이 특정 부분만을 변경하는 것이 가능하다.
   ex. ID중복 검사, 댓글작성

   동기 - 페이지가 전환, 
   클라이언트에 요청하고 서버가 응답하고 나서 클라이언트가 다시 요청할 수 있음   

   비동기 - 페이지가 전환되지 않고 응답받을 수 있음   
   클라이언트가 요청하면 서버가 응답하지 않더라도 다른 요청을 클라이언트가 할 수 있음   

1. # Ajax의 장단점
   장점   
   웹페이지 속도가 향상된다.(필요한 데이터만 리로드하면 되니까!)   
   서버의 처리가 완료될 때 까지 기다리지 않고 처리 가능하다.   
   서버에서 Data만 전송하면 되므로 코딩의 양이 줄어든다.   

   단점   
   히스토리 관리가 안된다.   
   페이지 이동없는 통신으로 인한 보안상 문제가 있을 수 있다.   
   연속으로 데이터를 요청하면 서버 부하가 생길 수 있다.   

1. # jQuery Ajax 메소드   
   $.ajax() : get, post 방식으로 Ajax를 수행한다.   
   $.get() : get 방식으로 Ajax을 수행한다.   
   $.post() : post 방식으로 Ajax을 수행한다.   
   $.getJSON() : get 방식으로 Ajax를 수행해 JSON 데이터를 가져온다.   
   $.getScript() : get 방식으로 Ajax를 수행해 Script 데이터를 가져온다.   
   $(selector).load() : Ajax를 수행한 후에 선택한 문서 객체안에 응답받을 파일(문자열)을 불러온다.   
