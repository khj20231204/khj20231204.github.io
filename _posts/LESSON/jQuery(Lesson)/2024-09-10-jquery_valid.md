---
layout: single
title: 유효성 검사
categories: jQuery(Lesson)
tag: []
author_profile: false
---

1. 유효성 검사
   jQuery에서는 jQuery의 문법이 있고, JS에서는 JS의 문법이 있습니다.   
   ```cs
      jQuery : $(this), val(), $.each("arr",function(i,v){})
      js : this, value, arr.forEach(function(v, i, arr){})
   ```   
   혼동해서 사용하면 error가 발생합니다.   

   ```html
      <html></html>
      <head>
      <title>radio 버튼을 이용한 설문 조사</title>
      <meta charset="utf-8">
      <script src="http://code.jquery.com/jquery-latest.js">
      </script>
      <script>
         $(document).ready(function(){
            $('form').submit(function(){

               /*
               jQuery : val()
               js : value
               */

               //text
               var textlen = $(":text").val();  //text가 1개밖에 없는 경우
               //if(textlen.length <= 0) console.log("text에 값 입력1");
               var textlen2 = $("input[id='txt']").val();
               //if(textlen2 == "") console.log("text에 값 입력2");
               
               //button : 유효성 검사할 거 없다
               //console.log($("input[temp='temporaryVar']").val());

               //radio
               var radioArr = $("input[name='season']");
               $.each(radioArr, function(i,v){
                  //console.log($(this).val()); //spring, summer, winder
                  //console.log(v.value);      //spring, summer, winder
                  //console.log($(this).is(':checked')) //true, false, false
                  //console.log(v.is(':checked')) //error, is는 jqeury문법, v는 js문법
               })
               $.each($("input[name='season']"), function(i,v){
                  //console.log($(this).val()); //spring, summer, winder
                  //console.log(v.value); //spring, summer, winder
                  //console.log($(this).is(':checked')) //true, false, false
                  //console.log(v.is(':checked')) //error, is는 jqeury문법, v는 js문법
               })
               $.each($("input[name='season']:checked"), function(i,v){  //checked된 것만 표시
                  //console.log($(this).val()); //winter ,checked된 것만 표시
                  //console.log(v.value); //winter ,checked된 것만 표시
                  //console.log($(this).is(':checked')) //true
                  //console.log(v.is(':checked')) //error, is는 jqeury문법, v는 js문법
               })
               $(radioArr).each(function(i,v){
                  //console.log($(this).val()); //spring, summer, winder
                  //console.log(v.value); //spring, summer, winder
                  //console.log($(this).is(':checked')) //true, false, false
                  //console.log(v.is(':checked')) //error, is는 jqeury문법, v는 js문법
               })

               //checkbox => 위에 radio버튼과 일치
               var checkboxArr = $("input[name='hobby']");
               $.each(checkboxArr, function(i,v){
                  //console.log($(this).val()) //reading, riding, bicycle
                  //console.log(v.value); //spring, summer, winder
                  //console.log($(this).is(':checked')) //true, false, false
                  //console.log(v.is(':checked')) //error, is는 jqeury문법, v는 js문법
               })

               //select
               var selectArr = $("select[name='tele']");
               $.each(selectArr,function(i,v){
                  console.log($(this).val()); //011, 1개만 출력, 선택하지 않으면 ""출력
                  console.log($(this).length); //1
               })

               return false;
            });
         })
      </script>	
      </head>
      <body>
         <form name="frm" method="post" action="return send.jsp">

            <!-- text -->
            <input type="text" id="txt">
            <br><br>
            <!-- button -->
            <input type="button" id="btn" temp="temporaryBtn" value="temporaryBtn">
            <br><br>
            <!-- radio -->
            <input type="radio" id="r1" name="season" value="spring">봄<br>
            <input type="radio" id="r2" name="season" value="summer">여름<br>
            <input type="radio" id="r3" name="season" value="winter">겨울<br>
            <br><br>
            <!-- "checkbox" -->
            <input type="checkbox" id="s1" name="hobby" value="reading">봄<br>
            <input type="checkbox" id="s2" name="hobby" value="riding">여름<br>
            <input type="checkbox" id="s2" name="hobby" value="bicycle">자건거<br>
            <br><br>
            <!-- select -->
            <select id="telephone" name="tele">
               <option value="">번호선택</option>
               <option value="010">010</option>
               <option value="011">011</option>
               <option value="019">019</option>
            </select>
            <br><br>
            <input type=submit value="전송">
         </form>

         </body>
      </html>
   ```