---
layout: single
title: 페이지 이동
categories: JSP(Lesson)
tag: []
author_profile: false
---



1. # 페이지 이동

   버튼 클릭시 바로 이동
   ```html
      <input type=button value="회원가입" id="register" onclick="location.href='memberform.html'">
   ```   
   
   <br>

   jsp페이지에서 바로 이동
   ```html
      <script>
         location.href="member/loginform.html";	
      </script>
   ```   

   <br>

   result가 1이면 loginform.html으로, 아니면 한 페이지 뒤로
   ```javascript
      if(result == 1){ //회원가입 성공
            //회원가입 성공시 알림창 띄우고 main으로 이동
      %>
         <script>
            alert("회원가입 성공");
            location.href="loginform.html";
         </script>
      <%		
         }else{ //회원가입 실패
      %>
         <script>
            alert("회원가입 실패");
            history.go(-1;)
         </script>
   ```   

   <br>

   리다이렉트 : 새로운 요청
   ```javascript
      response.sendRedirect("first.jsp?name=test");
   ```   
   이전 요청의 정보(request, session)는 유지되지 않습니다. 이전 요청의 정보(request, session)는 유지되지 않습니다.   

   <br>

   포워드 : 전달
   ```javascript
      <jsp:forward page="forwardTo.jsp"/>  
   ```
   클라이언트는 한 번의 요청만 하기 때문에 이전 요청의 정보(request, session)가 유지됩니다. 같은 서버 내의 페이지로만 이동할 수 있습니다.   