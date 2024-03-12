---
layout: single
title: (HTML)textarea&label
categories: CSS&HTML
tag: []
---

1. # textarea
   __다중 줄 입력 태그__   
   ```html
      <textarea>원하는 글을 여기에 &#13; 작성하세요</textarea>
   ```   
   <textarea style="background:yellow">원하는 글을 여기에 &#13; 작성하세요</textarea>  

   __rows 속성을 통해 줄 수 설정__   
   ```html
      <textarea rows="4">rows로 크기 지정</textarea>
   ```   
   <textarea rows="4" style="background:yellow">rows로 크기 지정</textarea>   

1. # label
   input 태그를 설명해주는 메세지를 추가합니다. label대신 span을 사용해도 기능과 시각적으로는 차이가 없습니다. 하지만 input 태그 설명의 용도로 개발이 되었기 때문에 웹 접근성을 향상과 for 속성을 사용할 수 있습니다.   
   ```html
      <label>이름</label>
      <input type="text">
   ```   
