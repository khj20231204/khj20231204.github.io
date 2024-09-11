---
layout: single
title: forward, include
categories: JSP(Lesson)
tag: []
author_profile: false
---

1. # forward
   request : http요청이 일어난 다음 페이지   
   request.setAttribute("name","홍길동");로 request생성   
   페이지가 넘어가는 곳까지가 request영역   
   페이지를 3번 넘기며 전달하면 3페이지가 request영역   
   __페이지를 넘기 때 forward로 넘겨야만 request값이 유지__    

   a.jsp -> b.jsp -> c.jsp   

   a.jsp   
   b.jsp페이지로    
   ```jsp
      <html>
         <body>
         <h1>Forward 사용법 예제</h1>

         <form method=post action="b.jsp">
            아이디 : <input type="text" name="id"><p>
            패스워드 : <INPUT TYPE="password" NAME="password"><p>
            <input type="submit" value="보내기">
         </form>

         </body>
      </html>
   ```   

   b.jsp   

   ```jsp
      <html>
         <body>
         <h2>포워딩하는 페이지: b.jsp</h2>

         <%
            request.setCharacterEncoding("utf-8");
         %>

         b.jsp의 내용 입니다.<br>
         화면에 절대 표시 안됩니다.

         <%	// request 객체로 공유 설정
            request.setAttribute("name","홍길동");
         %>
         
         <jsp:forward page="c.jsp"/>  

         </body>
      </html>
   ```   

   c.jsp   
   ```jsp
      <html>
         <body>
         <h2>포워딩되는 페이지: c.jsp</h2>

         <%
            String id = request.getParameter("id");
            String password = request.getParameter("password");
         %>

         <b><%=id%></b>님의<p>
         패스워드는 <b><%=password%></b>입니다.

         <jsp:forward page="d.jsp"/>  

         </body>
      </html>

   ```   

   forward로 값 넘기기   
   ```jsp
      <jsp:forward page="<%=selectedColor+\".jsp\"%>">
         <jsp:param name="selectedColor" value="<%=selectedColor%>"/>
         <jsp:param name="name" value="<%=name%>"/>
      </jsp:forward>
   ```    

1. # include   
   ```jsp
      <jsp:include page="includeSub2.jsp">
         <jsp:param name="siteName" value="<%=siteName1%>"/>
      </jsp:include>
   ```   
   siteName값을 includeSub2.jsp파일에 입력 후 includeSub2.jsp파일을 불러옵니다.   

   