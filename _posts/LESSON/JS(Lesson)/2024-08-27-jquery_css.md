---
layout: single
title: jQuery 사용법
categories: jQuery(Lesson)
tag: []
author_profile: false
---

1. # 선택자
   jQuery 선택자 종류   
   전체 : $("*")   
   태그 : $("태그명")   
   아이디 : $("#id 명")   
   클래스 : $(".class 명")    
   jQuery로 css 적용   
   .css( propertyName ) : 속성명으로 속성값을 구해온다.   
   .css( propertyName, value ) : 속성에 속성값을 설정한다.   
   ex) li.css(‘color’, ‘red’) : li 태그에 color를 red로 설정한다.   

   ```html
      <script>
         $(document).ready(function(){
            $('ul #first').css({"color":"red"}).css("fontSize","20px").css("backgroundColor","gray");
            $('#second').css("color","blue").css("fontWeight","bold")
            $('ul .third').css("backgroundColor","yellow");
            $('#fourth, .fifth').css("color","green");
            $('li:nth-child(6)').css({'color':'orange'});
         });
      </script>

      <ul>
         <li id="first">테스트 테스트 테스트 테스트 테스트</li>
         <li id="second">테스트 테스트 테스트 테스트 테스트</li>
         <li class="third">테스트 테스트 테스트 테스트 테스트</li>
         <li id="fourth">테스트 테스트 테스트 테스트 테스트</li>
         <li class="fifth">테스트 테스트 테스트 테스트 테스트</li>
         <li class="sixth">테스트 테스트 테스트 테스트 테스트</li>
      </ul>
   ```   
   속성과 속성값을 css("A","B")와 같이 `,`로 구분할 수 있고, css({'color':'red'})와 같이 `{}`와 `:`로도 구분할 수 있습니다.   

   __*css로 배경색 적용시 backgroundColor(o), backgroundcolor(x), background(o)__   

1. # css적용
   ```html
      <script>
         $(document).ready(function(){
            $('li').css("color","red").css("font-size","20px").css("background","gray");
         });
      </script>
   ```   
   css("속성","속성값")으로 설정하며 css를 계속 나열하여 적용할 수 있습니다.   

1. # html, text
   ```html
      <script>
         $(document).ready(function(){
            var text = $('h1').text();	//모든 h1태그의 내용을 읽어온다.
            var html = $('h1').html();	//첫번째 h1태그의 내용만 읽어온다.
            
            console.log('text:'+text);
            console.log('html:'+html);
            
            $('h2').text('자바스크립트<br>연습');	//텍스트 그대로 출력
            $('h3').html('자바스크립트<br>연습');  //html 적용되어 출력
         });
      </script>

      <h1>javascript연습</h1>
      <div>중간 나누기</div>
      <h1>jQuery연습</h1>
      
      h2 text:<h2></h2>
      h3 html:<h3></h3>


      실행 결과 :
      text:javascript연습jQuery연습
      html:javascript연습

      h2 text:
      자바스크립트<br>연습

      h3 html:
      자바스크립트
      연습
   ```   

1. # each함수 사용

   배열 가져오기   
   ```html
      <script>
         $(document).ready(function(){
            var list = ['야구','축구','농구','배구','수영'];
         
            //for문을 돌면서 index값 증가, index에 따라 value값 가져오기
            $.each(list, function(index, value){
               console.log("index:"+index);
               console.log("value:"+value);
               
               $('ol').append('<li>' + value + '</li>');
            });
         });
      </script>

      <body>
         <ol></ol>
      </body>
   ```

   객체 가져오기   
   ```html
      <script>
         $(document).ready(function(){
            var array = [{name:"naver", link:"http://www.naver.com"},
                  {name:"kakao", link:"http://www.kakao.com"},
                  {name:"google", link:"http://www.google.com"}];
            
            var output = "";
            $.each(array, function(index, value){
               output += "<a href="+ value.link + "><h1>" + value.name + "</h1></a><br>";
            });	
            
            $('div:first-child').html(output);
            
         });
      </script>

      <div></div>
      <div></div>
   ```   
   value로 객체의 프로퍼티를 가져옵니다. value. 으로 각각의 키와 값에 접근을 합니다.    
   value.name : name에 접근   
   value.link : link에 접근   

1. # attr
   attr()함수는 속성값을 가져오고 변경하는데 사용합니다.   
   ```javascript
      .attr(attributeName) : 속성명으로 속성값을 구해온다.
      .attr(attributeName, value) : 속성에 속성값을 설정한다.

      $("img").attr("src","sea.jpg")
               .attr("title","바다")
               .attr("width",150)
               .attr("height",150);
   ```   

   a href태그를 눌러도 화면이 넘어가지 않는 명령어   
   ```html
      <script>
         $(document).ready(function(){
            $('a').click(function(){
               $('img').attr("src","img/flower.jpg");
               
               return false; //a href가 실행 안됨, 화면이 img/sea.jpg로 넘어가는 걸 막음
            });
         });
      </script>

      <a href="img/sea.jpg">a2 화면 변경</a><br><br>
      <img src="img/building.jpg">
   ```   
   return false; 명령어가 화면이 넘어가는 걸 막자줍니다.

1. # eq필터
   ```javascript   
      <script>
         $(document).ready(function(){
            
            //a태그가 많아 구별이 안되는 경우
            //eq필터 : 특정 태그 안에서 태그의 순서를 구해주는 필터 선택자
            $("a:eq(0)").click(function(){
               $('img').attr("src","img/flower.jpg").attr("title","껏");
               
               return false;
            });
         
            $("a:eq(1)").click(function(){
               $('img').attr("src","img/sea.jpg").attr("title","빠다");
               
               return false;
            });
         });
      </script>
      <ul>
         <li><a href="img/flower.jpg">껏</a></li>
         <li><a href="img/sea.jpg">빠다</a></li>
      </ul>	
      <p><img src="img/flower.jpg" title="꽃"></p>
   ```   

1. # 

