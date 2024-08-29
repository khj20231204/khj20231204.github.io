---
layout: single
title: jQuery연결과 기초 함수
categories: jQeury(Lesson)
tag: [toggle, hide, show, select]
author_profile: false
---

1. # 설치방법
   1) http://www.jquery.com 접속후 다운로드 받아서 사용   

   2) CDN(Content Delivery Network) 방식   
   -사용자에게 간편하게 라이브러리를 제공하는 방식을 의미함   
   -구글, 마이크로소프트, jQuery측에서 사용자가 jQuery를 편리하게 사용할 수 있도록 라이브러리를 제공함   

   Uncompressed 버전   
   ◯◯.js 파일   
   
   Compressed 버전   
   ◯◯.min.js 파일   
   ◯◯.min.js 파일은 Minified 버전 (용량이 세배 이상 차이가 남)   
   Minified 버전은 파일의 용량을 최소화하려고 압축한 파일   

1. # 사용법
   ```javascript   
      $(document).ready(function(){
         alert("출력성공");
      });
		
		jQuery(document).ready(function(){
			alert("출력성공2");
		});

      $(function(){
         alert("출력성공3");
      });
   ```   
   $는 jquery함수를 말합니다. document는 현재 문서가 되며, $(document).ready : jqeury로 문서가 준비되면.. 이란 뜻입니다. jquery는 모두 함수로 이루어져 있습니다.

   `$(documnet).ready(functio(){});`는 `jQuery(document).ready(function(){});`와 같은 표현입니다. $는 jQuery 함수가됩니다.   
   `$(documnet).rady(function(){});`를 간단히 나타낸 것이 `$(function(){});` 입니다. 3가지 전부 jqeury를 실행하기 위해 가장 먼저 선언하는 방식으로 사용할 수 있습니다.   

   <span style="font-weight:bold">*toggle, val, show, hide등은 명령어가 아니라 함수이기 때문에 항상 <span style="color:red">()</span>가 붙습니다.</span>   
   <span style="font-weight:bold">*$('div').click(), $('select').change() 등 이벤트 등록시엔 <span style="color:red">on이 붙지 않습니다.</span></span>   

1. # 외부 jqeury 연결
   ```javascript
      <script src="연결파일.js"></script>
   ```   
   외부 js 연결파일을 script의 src로 가져옵니다. jquery는 자바스크립트 파일 외부 연결과 같습니다.   

   예)   
   ```html
      <head>
      <meta charset="UTF-8">
      <title>Insert title here</title>
      <script src="http://code.jquery.com/jquery-latest.js"></script> <!-- jquery CDN -->
      <script src="scripts.js"></script>  <!-- 외부 연결파일 -->
      </head>
      <body>
         <div id="sample1">이 div를 지우겠다</div>
         div 태그 안에 들어 있는 내용이 지워졌다.
      </body>
      </html>
   ```   

   scripts.js파일   
   ```js
      $(function(){
         $('#sample1').hide();
      })
   ```   
   외부 연결파일은 `$(function(){})`으로 jqeury함수 선언부터 시작해야합니다.

1. # 이벤트와 hide, show
   ```html
      <script>
         $(document).ready(function(){
            $('div').hide();	
            
            //id값이 b1인 버튼태그를 구해온다
            $('#b1').click(function(){
               $('#sample1').show();
            });
            
            $('#b2').click(function(){
               $('#sample1').hide();
            });
         });
      </script>

      <div id="sample1">이 div를 지우고 싶다.</div>
      div태그 안에 들어있는 내용이 지워졌어요
      <br>
      <button type="button" id="b1">출력</button>
      <button type="button" id="b2">숨기기</button>
   ```

1. # select박스 이벤트
   ```html
      <script>
         $(document).ready(function(){
            $('div').hide();
            
            $('select').change(function(){
               var v = $('select').val();
               
               if(v == 1){
                  $('#sel01').show();
                  $('#sel02').hide();	
               }else{
                  $('#sel01').hide();
                  $('#sel02').show();
               }
            });
         });
      </script>

      <select style="width:100px;"> <!-- select는 style의 width로 크기 조절 -->>
         <option value="1">1번</option>
         <option value="2">2번</option>
      </select>
      <div id="sel01">
         <input type="text">
      </div>
      <div id="sel02">
         <textarea rows="10" cols="10"></textarea>
      </div>
   ```   

1. # toggle
   ```html
      <script>
         $(document).ready(function(){
            $('button').click(function(){
               $('div').toggle();
            })
         });
      </script>

      <button>start</button>
      <div>출력1</div>
      <div>출력2</div>
      <div>출력3</div>
   ```   

1. # 외부 파일 연결
   ```html
      <script src="http://code.jquery.com/jquery-latest.js"></script>
      <script src="login.js"></script>
   ```   
   jQuery역시 자바스크립트와 같이 src로 외부 파일을 불러옵니다.   
   단, jQuery 라이브러리 이후에 외부 파일src를 입력해야 합니다.   