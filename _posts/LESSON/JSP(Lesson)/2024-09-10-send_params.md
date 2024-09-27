---
layout: single
title: 파라미터 전달
categories: JSP(Lesson)
tag: []
author_profile: false
---

1. # 
   board.jsp   
   ```cs
      <%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
         
      <%
         request.setCharacterEncoding("utf-8");

         //text
         String name = request.getParameter("name");
         System.out.println(name);
         
         //select(3항목) name값으로 접근, value값을 가져옴
         String select = request.getParameter("blood");
         System.out.println(select);
         
         //radio(2항목) name값으로 접근, value값을 가져옴
         String radio = request.getParameter("gender");
         System.out.println(radio);
         
         //checkbox(3항목)
         String[] checkbox = request.getParameterValues("hobby");
         for(String s : checkbox){
            System.out.println(s);
         }

         //content
         String content = request.getParameter("content")

         //replace("\n", "<br>"); \n을 <br> 태그로 치환 시킨다.
         //\n : textarea안에서 줄바꿈
         String contents = request.getParameter("content").replace("\n","<br>");
      %>

      작성자 : <%= name %><br>
      비밀번호 : <%= select %><br>
      제목 : <%= radio %><br>
      내용1 : <%= content %><br>
      내용2 : <pre><%= content %></pre>
         <%-- <pre> 입력된 내용 그대로 출력 --%>
      내용3 : <%= contents %>

      //html파일
      <form action="forwardForm2.jsp" method="post">
         <input type="text" name="name" id="name">
         <br><br>
         <select name="blood" id="sel">
            <option value="">혈액형 선택</option>
            <option value="a">A형</option>
            <option value="b">B형</option>
            <option value="b">B형</option>
         </select>
         <br><br>
         <input type="radio" name="gender" id="gender" value="male">남자
         <br>
         <input type="radio" name="gender" id="gender" value="female">여자
         <br><br>
         <input type="checkbox" id="s1" name="hobby" value="reading">봄<br>
         <input type="checkbox" id="s2" name="hobby" value="riding">여름<br>
         <input type="checkbox" id="s2" name="hobby" value="bicycle">자건거<br>
         <br><br>
         <input type="submit">
      </form>
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
