---
layout: single
title: Application, Session, PageContext
categories: JSP(Lesson)
tag: []
author_profile: false
---

1. # request, application
   page : 한 페이지   
   
   session : 로그인하고 로그아웃까지   
   
   request : http요청이 일어난 다음 페이지   
   request.setAttribute("name","홍길동");로 request생성   
   페이지가 넘어가는 곳까지가 request영역   
   페이지를 3번 넘기며 전달하면 3페이지가 request영역   

   application : 하나의 애플리케이션   

   ```jsp
      <%
         request.setCharacterEncoding("utf-8");
         String name = request.getParameter("name");
         String id = request.getParameter("id");
         if (name != null && id != null) {
            application.setAttribute("name", name);
            application.setAttribute("id", id);
         }
      %>

      <tr>
			<td>이름</td>
			<td><%=application.getAttribute("name")%></td>
		</tr>
      <tr>
			<td>아이디</td>
			<td><%=application.getAttribute("id")%></td>
		</tr>
   ```
   
1. # session
   ```jsp
      <%
         request.setCharacterEncoding("utf-8");
         String email = request.getParameter("email");
         String address = request.getParameter("address");
         String tel = request.getParameter("tel");
         session.setAttribute("email", email);
         session.setAttribute("address", address);
         session.setAttribute("tel", tel);

         String name = (String) application.getAttribute("name");
      %>

      <tr>
			<td>email</td>
			<td><%= session.getAttribute("email") %></td>
		</tr>
		<tr>
			<td>address</td>
			<td><%= session.getAttribute("address") %></td>
		</tr>
   ```

1. # pageContext
   ```jsp
      <body>
      <%
         pageContext.setAttribute("pageScope", "pageValue");
         request.setAttribute("requestScope", "requestValue");
      %>

         pageValue = <%=pageContext.getAttribute("pageScope") %><br>
         requestValue = <%=request.getAttribute("requestScope") %>
      </body>
   ```

