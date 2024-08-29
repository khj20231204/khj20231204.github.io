---
layout: single
title: jQuery on,text,select,checkbox
categories: jQuery(Lesson)
tag: []
author_profile: false
---
//javascript, jquery text, radio, checkbox value,val
1. # select, text
   ```javascript
      <script>
         $(document).ready(function(){
            $('#email').change(function(){   
               var v = $(this).val();  //val()로 
               
               if(v != ""){
                  $('#domain').attr('readonly',true); //true는 '나 "를 붙이지 않습니다.
                  $('#domain').attr('readonly','readonly');

                  $('#domain').val(v);
               }else{
                  $('#domain').attr('readonly',false);
                  $('#domain').removeAttr('readonly'); 

                  $('#domain').val('').focus();
               }
            });
         });
      </script>
      EMail :
      <input type="text" size="10" id="mailid">@
      <input type="text" size="15" id="domain">
      <select id="email">
         <option value="">직접입력</option>
         <option value="naver.com">네이버</option>
         <option value="daum.net">다음</option>
         <option value="gamil.com">구글</option>
      </select>
   ```   
   select 태그에 change 이벤트를 적용해도 this로 가져오는 값은 option의 value값 입니다.   
   input type="text"에 값을 가져올 땐 val(), 입력 시엔 val('값 입력');   
   attr값으로 readonly 속성을 설정하는데 readOnly로 O가 대문자로 사용해도 되고 소문자로 사용해도 됩니다.   
   
1. # sumbit 버튼
   ```html
      <script>
         $(document).ready(function(){
            $('#myform').submit(function(){  //myform에서 submit을 실행
            //$('#sub').submit(function(){) 다음과 같이 submit버튼의 id를 가져와서 이벤트를 추가하면 안됨
               if($('#name').val() == ''){
                  alert('이름을 입력하세요');
                  $('#name').focus();
                  return false;
               }
               
               if($('#email').val() == ''){
                  alert('email을 입력하세요');
                  $('#email').focus();
                  return false;
               }
            });
         });
      </script>
      <form id="myform" method="post" action="send.jsp">
         이름 : <input type="text" size="10" id="name"><br>
         EMail : <input type="text" size="20" id="email"><br>
            
         <input type="submit" value="전송" id="sub">
      </form>
   ```   
   sumbit버튼을 누를 시 유효성 검사 후 페이지를 넘기기 위해서 __form에서 submit이벤트를 실행합니다.__   

1. # on() 메소드
   on() 메소드를 이용하여 이벤트를 연결합니다.      
   $(selector).on( eventName, function() { } );   
   $(‘#box’).on( ‘click’, function() { } ); - click 이벤트   
   $(‘#box’).on( ‘mouseover’, function() { } ); - mouseover 이벤트   
   $(‘#box’).on( ‘mouseout’, function() { } ); - mouseout 이벤트   

   ```javascript
      <script>
         $(document).ready(function(){
            $('#box').css({background:'yellow', width:100, height:100})
               .on('click', function(){
                  $(this).css('backgroundColor','red');
               }).on('mouseover',function(){
                  $(this).css('backgroundColor','orange');
               }).on('mouseout', function(){
                  $(this).css('backgroundColor','blue');
               });
         });
      </script>

      <div id="box"></div>
   ```   

1. # form객체
   form객체 `<form name=“myform” method=“post” action=“send.jsp”>`   
   form객체의 속성   
   id : form객체의 id를 설정하는 속성   
   name : form객체의 name을 설정하는 속성   
   method : 값을 전달하는 방식을 설정하는 속성( get or post)   
   action : 값이 전달될 url 주소를 설정하는 속성   

   ```html
      <script>
         $(document).ready(function(){
            $("#frm").submit(function(){ //form에 submit을 추가
               var v = $(":text").val();
               if(v == ""){
                  alert("글자 입력");
                  $("input[myval='my']").focus();
                  return false;
               }
            });
         });
      </script>

      <form id="frm" method="get" action="send.jsp">
         <input type="text" myval="my">
         <input type="submit" value="전송">
      </form>
   ```

1. # text객체
   text객체 메소드   
   val() 메소드는 입력, 선택 양식에서만 사용할 수 있다.   
   val() : text 객체의 값을 구해온다.   
   val( value ) : text 객체에 값을 설정한다.   
   $('input').val() : input 태그 안의 값을 구해온다.   
   $('input').val('가위') : input 태그 안에 ‘가위’ 를 설정한다.   

   text() 메소드   
   text() 메소드는 특정 태그 안의 값을 구해오거나,값을 설정할 수 있다.   
   text() : 특정 태그 사이의 값을 구해온다.   
   text( value ) : 특정 태그 사이에 값을 설정한다   

1. # checkbox객체
   *필터 선택자 `:checkbox` => input type=checkbox 로 되어있는 태그를 모두 구해오는 필터 선택자   
   prop() 메소드 : 속성(property)에 속성값을 설정하거나, 속성으로 속성값을 구해오는 역할을 하는 메소드
   prop( propertyName )   
   prop( propertyName , value )   
   prop("checked", true ) : checkbox에 체크를 활성화   
   prop("checked", false ) : checkbox에 체크를 해제   
   removeProp("checked") : checkbox에 체크를 해제   

   ```html
      <script>
         $(document).ready(function(){
            var v = $("input[name='hobby']");   //input타입을 태그로 가지면서 name속성이 hobby인 모든 객체를 가져옵니다.
            alert(v.length);
            
            $(":button[value='전체선택']").click(function(){ //type이 button이면서 value속성이 '전체선택'인 것을 클릭했을 때
               $(":checkbox").prop('checked',true);	
            });
            
            $(":button[value='전체해지']").on('click',function(){ //type이 button이면서 value속성이 '전체해지'인 것을 클릭했을 때
               $(":checkbox").prop('checked',false);
            });
         });
      </script>

      <input type="checkbox" name="hobby">등산
      <input type="checkbox" name="hobby">축구
      <input type="checkbox" name="hobby">농구
      <br><br>
      <input type="button" value="전체선택">
      <input type="button" value="전체해지">
   ```   

1. # radio객체
   radio객체   
   radio : input type=radio 로 되어있는 태그를 모두 구해오는 필터 선택자   
   `is() 메소드` : radio버튼이나 checkbox의 선택 여부를 판별할때 사용되는 메소드 선택되면 true, 선택되지 않으면 false를 리턴한다.   
   `is(":checked")`   
   `$(":radio").is(":checked")` : 모든 radio버튼을 구해와서 선택 여부를 판별한다   

   ```html
      <script>
         $(document).ready(function(){
            //배열로 가져오기
            $("#check01").click(function(){
               var arr = $(":radio");
               
               var len = arr.length;
               var count = 0;
               $.each(arr, function(i,v){
                  if(!v.checked)count++;
               });
               
               if(count == len) alert("체크하시오");
            });
            
            //is(":checked") 사용
            $("#check02").click(function(){
               alert("남자:" + $("input[value='man']").is(":checked"));
               alert("여자:" + $("input[value='woman']").is(":checked"));
            });
         });
      </script>

      <input type="radio" name="gender" value="man">남자
      <input type="radio" name="gender" value="woman">여자
      <br>
      <button type="button" id="check01">라디오 체크01</button>
      <button type="button" id="check02">라디오 체크02</button>
   ```   

1. # select객체
   change이벤트와 val()함수, attr()함수를 사용합니다.

   ```html
      <script>
         $(document).ready(function(){
            $('#sel').change(function(){
               
               var v = $(this).val();
               
               if(v == 10 || v == ""){
                  $("#txt").attr('readOnly', true).val('').css('backgroundColor','lightgray');
               }else{
                  $("#txt").attr('readOnly', false).val('').css('backgroundColor','white').focus();
               }
               
            });
         });
      </script>
      <select id="sel">
         <option value="">나이선택</option>
         <option value="10">10대</option>
         <option value="20">20대</option>
         <option value="30">30대</option>
      </select><br><br>
      좋아하는 술 : <input type="text" id="txt" readOnly='true' style="background-color:lightgray">
   ```

1. # 정규표현식
   정규 표현식 특정한 규칙을 가진 문자열의 집합을 표현하는 데 사용하는 형식언어입니다.   

   정규 표현식   
   var pattern = /^[a-z]+[a-z0-9_]$/; 영문소문자, 숫자,언드바(_)만 사용가능   
   var num = /^[0-9]+$/; 숫자만 사용가능   

   일반적인 아이디 체크   
   `/^`는 처음을 나타내면 `$/`는 표현식의 끝을 나타냅니다.   
   `[a-z]` a~z까지 소문자만 허용됩니다.   
   `+` 앞에 기호 a~z까지 __적어도 1개 이상__ 나와야합니다.   
   `[a-z0-9_]` a~z와 0~9, 그리고 `_(언더바)` 를 허용합니다.   

   test() - 자바스크립트에서 제공하는 정규표현식 체크하는 함수입니다.      
   정규 표현식의 형식에 맞지 않으면 false 값을 리턴한다.   
   if( !pattern.test(id) )   
   if( !num.test(passwd) )   

   ```html
      <script>
         $(document).ready(function(){
            $('form').submit(function(){
               //정규 표현식
               var pattern = /^[a-z]+[a-z0-9_]$/;
               //영문 소문자, 숫자, 언더바만 사용가능
               var num = /^[0-9]+$/;
               //+는 1회사용 의무
               
               var id = $.trim($('#id').val());
               var passwd = $.trim($('#passwd').val());
               
               var a = document.getElementById("id");
               console.log(a.value);
               
               if(id == ''){
                  alert('ID를 입력 하세요.');
                  $('#id').focus();
                  return false; 
               }else if(!pattern.test(id)){
                  alert("비밀번호 재설정")
                  return false;
               }
               
               if(passwd == ''){
                  alert('비밀번호를 입력하라');
                  $('passwd').focus();
                  return false;
               }else if(!num.test(passwd)){
                  alert('비밀번호는 숫자만 가능');
                  $('#passwd').val('').focus();
                  return false;
               }
               
            });
         });
      </script>
      <form method="post" action="send.jsp">
         ID : <input type="text" id="id"><br>
         비밀번호 : <input type="text" id="passwd">	
         <input type="submit" value="전송">
      </form>
   ```
   