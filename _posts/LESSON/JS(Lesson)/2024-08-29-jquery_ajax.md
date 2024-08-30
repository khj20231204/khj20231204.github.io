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

1. # load()메소드 
   ```html
      <script>
         $(document).ready(function(){
            $('#menu1').click(function(){
               
               //load 함수를 이용해서 menu.html 문서 전체를 읽어와서 
               //id가 message1인 태그 사이에 출력한다.
               $('#message1').load('menu.html');
               //$('#message2').load("sample1.txt");
            });
            
            $('#menu2').click(function(){
               
               //load 함수를 이용해서 menu.html 문서 전체를 읽어와서 
               //id가 message2인 태그 사이에 출력한다.
               $('#message2').load('menu.html li');
               
            });
         });
      </script>
   ```   
   html, txt, xml, json 형식의 파일들을 load로 가져올 수 있습니다.   

1. # ajax()메소드로 html불러오기

   서버에 get, post 방식 모두 요청할 수 있는 함수이다.   
   ```js
      $.ajax({   
         url : "전송 페이지",
         type : "전송 방식(get, post방식),
         data : "전송할 데이터",
         dataType : "요청한 데이터입("html","xml","json","text"),
         success : function(result){
         콜백함수로 돌려 받은 후 실행될 문장;
         }
      });
   ```   
   웹 브라우저에 출력되는 결과가 콜백함수로 리턴 됩니다.   
   url와 success만 필수입니다. 두 가지 옵션이 있어야 데이터를 넘겨주고 받을 수 있습니다.   
   type, data, dataType은 필수는 아니지만 데이터를 가공하거나 특별한 처리를 할 경우 필수가 됩니다.   

   type : 데이터를 서버로 전송하지 않고, 단순히 받기만 하는 경우 생략가능합니다.   
   data : 서버로 전송할 데이터가 있는 경우 사용하고 없으면 사용하지 않습니다.   
   dataType : 서버에서 받은 데이터를 그대로 사용할 경우 생략할 수 있지만, 파싱이나 형식을 변환해야 하는 경우 작성을 해야합니다.   

   type은 데이터 __전송__ 방식입니다. data는 서버쪽에 __전송__ 할 데이터 입니다.   
   dataType은 서버쪽에서 __전송 받은__ 데이터 타입입니다.  

   ```javascript
      <script>
         $(document).ready(function(){
            $("#menu1").click(function(){ //메뉴보기1 클릭
               $.ajax({
                  url: 'menu.html',	//서버에 요청할 파일명
                  type: 'post',		//전송방식 설정
                  dataType: 'html',	//요청한 데이터 타입
                  
                  //서버로부터 응답받은 데이터는 콜백함수의 매개변수로 전달된다.
                  success : function(result){
                     alert(result);
                     
                     //콜백함수로 돌려받은 data를 id가 message1인 태그사이에 출력
                     $('#message1').html(result);
                     $('#message2').html($(result).find('li'));
                  }
               });
            });
         });
      </script>

      <div>
         <a href="#" id="menu1">메뉴 보기1</a>
         <span id="message1"></span>
      </div>
      <div>
         <a href="#" id="menu2">메뉴 보기2</a>
         <span id="message2"></span>
      </div>
   ```   
   콜백 함수로 받은 html 결과값 result를 다시 처리할 때 `$(result)`를 사용합니다.   

1. # post()메서드로 jsp로 값 넘기고 받기
   ```javascript
      <script>
         $(document).ready(function(){
            $('#b1').click(function(){
               
               //$.post("요청할 파일명","전달할 데이터","콜백함수");
               $.post('welcome.jsp', 
                     {'username' : $('#username').val() },
                     function(msg){
                        alert(msg);
                        $('#message').html(msg);
                     }
               );
            });
         });
      </script>

      이름입력:
      <input type="text" id="username"><br>
      <input type="button" value="전송" id="b1"><br>
      <br><br>
      <div id="message"></div>
   ```   
   post의 데이터에서 username은 넘겨주는 값입니다. welcome.jsp파일로 넘겨줄 변수가 됩니다.   

   welcome.jsp부분   
   ```jsp   
      <body>
         <!-- 웹브라우저에 출력되는 결과가 콜백함수로 리턴된다. -->
         환영합니다. <%=request.getParameter("username") %>님 <br>
      </body>
   ```   
   jsp에서 getParameter로 username값을 받습니다. 이것을 html태그로 화면에 출력하게 되고 출력화면이 클라이언트의 콜백함수로 리턴됩니다.   

1. # ajax의 post방식으로 jsp에 값 넘기고 받기
   ```javascript
   <script>
      $("#btn2").click(function(){
			$.ajax({
				url : 'welcome.jsp',
            type : 'post',
				data : {username : $("#username").val()},
				success : function(data){
					$("#msg2").html(data);
				}
			});
		});
   </script>
   <input type="button" id="btn2" value="ajax 전송">
	<div id="msg2"></div>
   ```   

1. # get()메서드로 xml파일 받기

   ```javascript
      <script>
         $(document).ready(function(){
            $("#btn").click(function(){
               
               $.get('item.xml',
                  function(data){
                     $("#treeData").append(
                           '<tr><td>id</td><td>name</td><td>price</td><td>description<td></tr>'
                           );
                     $(data).find('item').each(function(){
                        
                        var item = $(this);
                        $('#treeData').append(
                        "<tr><td>"+ item.attr('id')+ "</td>" + 
                        "	 <td>" + item.attr('name') + "</td>" +
                        "	 <td>" + this.find('price').text() + "</td>" +
                        "	 <td>" + this.find('description').text() + "</td></tr>"	
                        );
                     });
               });
            });
         });
      </script>
   ```

1. # get()메서드로 json파일 받기

   ```javascript
      <script>
         $(document).ready(function(){
            
            $.getJSON('item.json', function(data, textStatus){
              
               $("#treeData").append("<tr><td>id</td><td>name</td><td>price</td><td>description</td></tr>")
               $.each(data, function(){
                  $('#treeData').append(
                        "<tr><td>" + this.id + "</td>" +
                        "	 <td>" + this.name + "</td>" +
                        " 	 <td>" + this.price + "</td>" + 
                        "    <td>" + this.description + "</td></tr>"
                        );
               });
            });
         });
      </script>
   ```   
   콜백함수의 매개변수로 받은 data와 textStatus에는 각각 다음과 같은 데이터가 입력됩니다.   
   data : 콜백함수로 서버에서 돌려받는 데이터   
   textStatus : 콜백함수로 잘 돌려 받으면 ‘SUCCESS’ 리턴   

1. # ajax로 json파일 받기

   ```javascript
      <script>
         $(document).ready(function(){
            
            $.ajax({
               url : "item.json",
               dataType : "json",
               success : function(data){
                  $("treeData").append("<tr><td>id</td><tr>name</td><td>price</td><td>description</td></tr>");
                  
                  $.each(data, function(){
                     var v =	"<tr><td>" + this.id + "</td>" +
                        "    <td>" + this.name + "</td>" +
                        "	 <td>" + this.price + "</td>" +
                        " 	 <td>" + this.description + "</td></tr>";
                        
                     $("#treeData").append(v);
                  });
               }
            });
         });
      </script>

      <table id="treeData"></table>
   ```