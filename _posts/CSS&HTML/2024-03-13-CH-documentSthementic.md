---
layout: single
title: (HTML)문서 구조화
categories: CSS&HTML
tag: []
---

1. # 구조화된 페이지
   검색 엔진이 검색을 할 때 div, table로 구성된 예전 HTML 파일에서 원하는 정보를 검색하기엔 정보와 의미가 부족했습니다. HTML5 이후 버젼부터 header, nav, section, aside, footer등 콘텐츠에 의미를 표현하는 시멘틱 태그를 사용한 시멘틱 웹이 개발되므로인해 웹 문서에 의미 정보를 더할 수 있었고, 이는 검색 엔진의 탐색이 더 쉽고 정확한 탐색 결과를 얻을 수 있었습니다. 이러한 검색의 이점을 활용하기 위해 구조화된 페이지가 필요하게 되었습니다.   
   *시멘틱 : 의미   

   `<header>` : 페이지나 섹션의 머리말을 표현   
   `<nav>` : 하이퍼링크를 모아놓은 섹션. 페이지 내 목차를 위해 사용   
   `<section>` : 문서의 장, 또는 절을 구성하는 역할   
   `<article>` : 본문과 연관되어 있지만 독립적인 콘텐츠를 담는 영역   
   `<aside>` : 주요 기사 옆에 짤막하게 곁들이는 관련 기사, 주로 삽입 어구로 논평이나 글을 담음   
   `<footer>` : 꼬리말로 저자나 저작권 정보를 표시   

   ```html
      <header>
         <h1> 제목 </h1>
      </header>
      <nav>
         <h2>목차</h2>
         <ul>
            <li></li>
            <li></li>
         </ul>
      </nav>
      <section> <!-- section안에 여러개의 article로 구성 -->
         <article id="내용1">내용1</article>
         <article id="내용2">내용2</article>
      </section>
      <aside>
         <h2>내용과 관련된 링크</h2>
      </aside> 
      <footer></footer>
   ```   
   주로 이런 형태로 구성하게 됩니다.   
   nav - section - aside   
   nav와 section과 aside는 이렇게 나란한 형태를 가지며 nav와 aside의 폭은 각각 15%, section이 폭은 70%를 주게 됩니다.   

1. # 시멘틱 블록 태그
   figure, details, summary

1. # 시멘틱 인라인 태그
   mark, time, meter, progresls