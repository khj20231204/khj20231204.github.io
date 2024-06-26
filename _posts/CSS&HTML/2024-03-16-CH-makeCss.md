---
layout: single
title: (CSS)스타일 시트 개요와 만들기
categories: CSS&HTML
tag: []
---

1. # css 구성
   ```css
      span {color:blue; font-size;30px;}
   ```   
   span : 셀렉터   
   color, font-size : 프로퍼티   
   blue, 30px : 값   
   
   - 셀렉터 : css스타일을 적용할 이름이나 규칙   
   - 프로퍼티와 값 : '프로퍼티:값'의 쌍으로 표현되며 세미콜론(;)으로 분리   

   ※ __셀렉터, 프로퍼티, 값 모두 대소문자를 구분하지 않습니다.__    
   

1. # css 만들기
   1) style 속성으로 스타일 시트 작성   
   2) `<style></style>` 태그에 스타일 시트 작성   
   3) 별도의 파일을 만들어 link태그나 @import로 불러 이용   

   *우선 순위 : style속성으로 직접 입력하는 경우 > `<style>`태그 사용 >  link태그나 @import 이용   

   1) style 속성으로 스타일 시트 작성   
   ```css
      <p style="color:red;font-size:20px">내용입력</p>
   ```   
   위에 3가지 방법 중 가장 우선순위가 높습니다. 해당 태크만 스탈이 적용됩니다.   

   2) `<style></style>` 태그에 스타일 시트 작성   
   ```html
      <head>
         <style>
            p {color:red; font-size:20px;}
         </style>
      </head>
   ```   
   `<style>`태그는 반드시 `<head>`내에서만 작성 가능합니다. 작성된 스타일 시트는 웹 페이지 전체에서 적용됩니다.   

   3) 별도의 파일을 만들어 link태그나 @import로 불러 이용   
   3-1)link이용   
   ```html
      /* 별도의 mystyle.css 파일 내부  */
      body {background-color:orange;}
      h1 {color:red}
   
      /* html 파일 */
      <!DOCTYPE html>
      <html>
         <head>
            <link href="mystyle.css" type="text/css" rel="stylesheet">
         </head>
         <body>
            <h1>제목</h1>
         </body>
      </html>
   ```   
   별도의 mystyle.css파일 배부에선 `<style>` 태그를 사용하지 않고 바로 내용옵니다.   

   link태그는 닫는 태그가 없습니다.   
   href : 외부 스타일시트 파일경로를 입력합니다.   
   type : 불러오는 파일이 css 형식임을 알려줍니다.   
   rel : 불러오는 파일이 스타일 시트임을 알려줍니다.   

   3-2)@import 이용   
   ```html
      /* 별도의 mystyle.css 파일 내부  */
      body {background-color:orange;}
      h1 {color:red}
   
      /* html 파일 */
      <!DOCTYPE html>
      <html>
         <head>
            <style>
               @import url(mystyle.css);
               /* @import url('mystyle.css'); ☜다음과 같이 작성 가능 
                  @import "mystyle.css"; ☜다음과 같이 작성 가능 */
            </style>
         </head>
         <body>
            <h1>제목</h1>
         </body>
      </html>
   ```   
   @import는 `<style>`태그 안에서 사용가능 합니다.   



