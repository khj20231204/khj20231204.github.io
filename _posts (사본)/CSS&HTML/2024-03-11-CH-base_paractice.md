---
layout: single
title: (HTML)기초 practice
categories: CSS&HTML
tag: []
---

1. # table
   table : 표 전체를 담는 컨테이너   
   caption : 표 제목   
   thead : 헤딩 셀 그룹   
   tfoot : 바닥 셀 그룹   
   tbody : 데이터 셀 그룹   
   tr : 행, 여러 개의 th, td 포함   
   th : 제목 셀   
   td : 데이터 셀   

   ```html
      <table>
      
         <caption>제목</caption>
      
         <thead>
            <tr><th>헤드1</th><th>헤드2</th></tr>
         </thead>

         <tfoot>
            <tr><td>바닥1</td><td>바닥2</td></tr>
         </tfoot>

         <tbody>
            <tr><td>바디1</td><td>바디2</td></tr>
         </tbody>
      
      </table>
   ```   
      <table>
         <caption>제목</caption>
         <thead>
            <tr><th>헤드1</th><th>헤드2</th></tr>
         </thead>
         <tfoot>
            <tr><td>푸트1</td><td>푸트2</td></tr>
         </tfoot>
         <tbody>
            <tr><td>바디1</td><td>바디2</td></tr>
         </tbody>
      </table>   

   검색 엔진은 표의 의미를 파악하기 위해 caption, thead, tfoot, tbody 태그를 찾기 때문에 이를 구분해서 생략하지 말고 적어주는 게 좋습니다. 또 tfoot는 tbody전에 나오는 것이 좋습니다. 웹 페이지가 프린트될 때 tbody 내용이 길어 여러 페이지에 걸치게 될 때, __헤드와 바닥을 각 페이지마다 위아래에 출력__ 하기 위함입니다. 

1. # 리스트   
   순서 있는 리스트(Ordered List) : ol   
   순서 없는 리스트(Unordered List) : ul   
   *ol과 ul 세부항목으로 li를 사용
   정의 리스트(definition list) : dl   
   *dl 세부항목으로 dt(defination title),dd(difination detail)사용

   - type : 마커의 종류
   type="1" : 1,2,3,...   
   type="A" : A,B,C,...   
   type="a" : a,b,c,...   
   type="I" : I,II, III, ...   
   type="i : i,ii, iii, ...   

   - start : 마커의 시작 값   
   예)start="4" : 4,5,6,...   

   ```html
      <ol type="A" start="3">
         <li>item1</li>
         <li>item2</li>
         <li>item3</li>
      </ol>

      <ul>
         <li>item1</li>
         <li>item2</li>
         <ul>
            <li>subitem1</li>
            <li>subitem2</li>
            <li>subitem3</li>
         </ul>
         <li>item3</li>
      </ul>

      <dl>
         <dt>정의 제목</dt>
         <dd>정의 내용입력</dd>
      </dl>
   ```   
   <ol type="A" start="3">
      <li>item1</li>
      <li>item2</li>
      <li>item3</li>
   </ol>
   <ul>
      <li>item1</li>
      <li>item2</li>
      <ul>
         <li>subitem1</li>
         <li>subitem2</li>
         <li>subitem3</li>
      </ul>
      <li>item3</li>
   </ul>
   <dl>
      <dt>정의 제목</dt>
      <dd>정의 내용입력</dd>
   </dl>

1. # id속성으로 앵커 만들기   
   `<a href="#앵커이름">`앵커이름에 해당하는 하이퍼링크를 만들고 클릭을 하면,   
   `<id="앵커이름">`id가 앵커이름인 태그 위치로 이동합니다.   

   ```html
      <a href="#chap1">챕터 1로 가기</a>
      <a href="#title1">제목 1로 가기</a>
      <p id="chap1">챕터 1</p>
      <h1 id="title1">제목 1</h1>
   ```   
   <a href="#chap1">챕터 1로 가기</a>   
   <a href="#title1">제목 1로 가기</a>   
   .<br>
   .<br>
   .<br>
   .<br>
   .<br>
   .<br>
   .<br>
   .<br>
   .<br>
   .<br>
   .<br>
   <h1 id="title1">제목 1</h1>   
   <p id="chap1">챕터 1</p>   
   
   다른 페이지의 앵커로도 연결이 가능합니다.   
   `<a href="student.html#chap1">` student.html페이지의 chap1위치의 앵커로 이동하게 됩니다.   

1. #  파일 다운로드 a의 download속성   
   `<a>`태그에 download속성을 사용하면 이미지, PDF, MP3, HTML파일, HWP파일, PPT파일 등 모든 파일을 다운로드 할 수 있습니다.   
   ```html
      <a href="../../imgs/CH/man_comic.png" download>이미지 다운로드</a>
   ```
   <img src="../../imgs/CH/man_comic.png" style="border:3px solid black;border-radius:9px;width:100px" download><sub><a href="../../imgs/CH/man_comic.png" download>이미지 다운로드</a></sub>   

1. # 요약
   2. HTML은 어떤 언어인가?   
   <span style="color:#E8F5FF">Hyper Text Markup Language의 약자입니다. 태그로 각 문서의 요소를 표현하여 웹 문서를 작성하는 언어입니다.</span>   

   2. img태그 속성의 종류는?   
   <span style="color:#E8F5FF">src, alt, width, height</span>   

   2. a태그 속성의 종류는?   
   <span style="color:#E8F5FF">href, target, download</span>   

   2. ifram태그 속성의 종류는?   
   <span style="color:#E8F5FF">src, srcdoc, name, width, height</span>   

   2. 웹 페이지의 제작자를 표현하기 위해  사용되는 태그는?   
   <span style="color:#E8F5FF">meta</span>
   
   2. 웹페이지를 만든 이유를  "자바에 대해 알려주려고"라고 웹 페이지에 내에 적어 놓고자 한다. 가장 적절한 태그는 무엇인가? 태그를 완성하라   
   <span style="color:#E8F5FF">`<meta name="description" content = "자바에 대해 알려주려고">`</span>   

   
   









