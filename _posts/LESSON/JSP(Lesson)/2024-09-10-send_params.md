---
layout: single
title: 파라미터 전달
categories: JSP(Lesson)
tag: []
author_profile: false
---

1. # 

   board.html파일 -> submit버튼 -> 유효성 검사 -> board.jsp

   board.html파일
   ```html
      <body>
      <form method="post" action="board.jsp">
      <table border=1 width=600 align=center>
         <caption>게시판</caption>
         <tr><th>작성자</th>  <!-- th : 가운데 정렬, 찐하게 출력 -->
            <td><input type=text size=30 id="writer" name="writer" placeholder="작성자명 입력"></td>
         </tr>
         <tr><th>비밀번호</th>
            <td><input type=password size=30 id="passwd" name="passwd" placeholder="2~8자 이내 입력"></td>
         </tr>
         <tr><th>제목</th>
            <td><input type=text size=60 id="subject" name="subject"></td>
         </tr>
         <tr><th>내용</th>
            <td><textarea rows="5" cols="50" id="content" name="content" placeholder="200자 이내로 입력"></textarea></td>
         </tr>
         <tr><th>파일첨부</th>
            <td><input type=file></td>
         </tr>
         <tr><td colspan=2 align=center>
               <input type=submit value="글작성">	 <!-- submit :전송기능 있는 버튼 -->
               <!-- <input type=button value="글작성2">  -->  <!-- button :전송기능 없는 버튼 -->
               <!-- <button>글작성3</button>	 -->			 <!-- 전송기능이 있는 버튼 -->
               <!-- <button type=submit>글작성4</button>  --> <!-- 전송기능이 있는 버튼 -->
               <!-- <button type=button>글작성5</button> -->  <!-- 전송기능이 없는 버튼 --> 
               <input type=reset value="취소">      <!-- 초기화 버튼 -->
            </td>
         </tr>
      </table>
      </form>

      </body>
   ```   

   board.js   
   ```js
      $(function(){
         $("form").submit(function(){
            if($.trim($("#writer").val()) == ""){
               alert("작성자명을 입력하세요.");
               $("#writer").focus();
               return false;
            }
            if($.trim($("#passwd").val()) == ""){
               alert("비밀번호를 입력하세요.");
               $("#passwd").focus();
               return false;
            }
            if($("#passwd").val().length <2 || 
               $("#passwd").val().length >8	){
               alert("비밀번호는 2~8자로 입력하세요");
               $("#passwd").val("").focus();
               return false;
            }
            if($.trim($("#subject").val()) == ""){
               alert("제목을 입력하세요.");
               $("#subject").focus();
               return false;
            }
            if($.trim($("#content").val()) == ""){
               alert("내용을 입력하세요.");
               $("#content").focus();
               return false;
            }
            if($.trim($("#content").val()).length > 200){
               alert("내용은 200자 이내로 입력하세요");
               $("#content").focus();
               return false;
            }
         });		
      });	
   ```
   
   board.jsp   
   ```cs
      <%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
         
      <%
         request.setCharacterEncoding("utf-8");

         String writer = request.getParameter("writer");
         String passwd = request.getParameter("passwd");
         String subject = request.getParameter("subject");
         String content = request.getParameter("content");

         //replace("\n", "<br>"); \n을 <br> 태그로 치환 시킨다.
         //\n : textarea안에서 줄바꿈
         String contents = request.getParameter("content").replace("\n","<br>");
      %>

      작성자 : <%= writer %><br>
      비밀번호 : <%= passwd %><br>
      제목 : <%= subject %><br>
      내용1 : <%= content %><br>
      내용2 : <pre><%= content %></pre>
         <%-- <pre> 입력된 내용 그대로 출력 --%>
         
      내용3 : <%= contents %>
   ```   
   
1. # response

   responseEx.jsp
   ```cs
      <%@ page contentType="text/html;charset=utf-8"%>

      <h1>Response 예제</h1>
      현재 페이지는  responseEx.jsp 페이지입니다.

      <%	// JSP에서 페이지 이동
         response.sendRedirect("first.jsp?name=test");
      %>
   ```   
   sendRedirect는 get방식으로만 데이터를 전송합니다. post방식은 다른 함수를 선택해야 합니다.

   first.jsp
   ```cs
      <%@ page contentType = "text/html; charset=utf-8" %>
      <%
         String str = request.getParameter("name");
      %>
      name : <%=str%>
   ```   

1. # out
   ```cs
      <%@ page contentType = "text/html; charset=utf-8" %>
      <html>
      <head><title>out 기본 객체 사용</title></head>
      <body>
      <%
         out.println("안녕하세요?<br>");  
         out.println("안녕하세요2?");
      %>
      <br>
      out 기본 객체를 사용하여 
      <%
         out.println("출력한 결과입니다.");
      %>
      </body>
      </html>
   ```   
   `<br>`태그는 println 안에서 사용하든지, 표현식(`<% %>`) 외부에서 사용해야 합니다.   
