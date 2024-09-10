---
layout: single
title: 내장 객체
categories: JSP(Lesson)
tag: []
author_profile: false
---

1. # JSP의 내장 객체
   __request__ : 클라이언트의 요청 정보를 저장합니다.   
   실제 타입 : javax.servlet.http.HttpServletRequest 또는 javax.servlet.ServletRequest

   __response__ : 응답 정보를 저장합니다.   
   실제타입 : javax.servlet.http.HttpServletResponse 또는 javax.servlet.ServletResponse   

   __session__ : HTTP 세션 정보를 저장합니다.   
   실제타입 : javax.servlet.jsp.HpptSession   

   __out__ : JSP 페이지가 생성하는 결과를 출력할 때 사용되는 출력 스트림입니다.   
   실제타입 : javax.servlet.JspWriter   

   pageContext : JSP 페이지에 대한 정보를 저장합니다.   
   실제타입 : javax.servlet.jsp.PageContext   

   application : 웹 어플리케이션에 대한 정보를 저장합니다.   
   실제타입 : javax.servlet.ServletContext   

   config : JSP에 대한 설정 정보를 저장합니다.   
   실제타입 : javax.servlet.ServletConfig   

   page : JSP페이지를 구현한 자바 클래스 인스턴스입니다.   
   실제타입 : java.lang.Object   

   exception : 예외 객체, 에러 페이지에서만 사용됩니다.   
   실제타입 : java.lang.Throwable   

   javax는 java의 확장 기능을 모아놓은 라이브러리로 서블릿과 같은 외부 기술과 특정 기술을 지원하는 라이브러리를 모아놓았습니다.   
   <a hef="https://javaee.github.io/javaee-spec/javadocs/">https://javaee.github.io/javaee-spec/javadocs/</a>   

1. # request 객체의 주요 메서드
   void setCharacterEncoding(String env) : 한글 인코딩 처리   

   String getParameter(String name) : name에 해당하는 파라미터 값을 구함   

   String[] getParameterValues(String name) : checkbox 같이 여러 개의 파라미터 값을 구함   

   String getRemoteAddr() : client의 IP주소를 구함   

   String getRequestURI() : 요청 URI를 구함   

   String getContextPath() : 현재 요청이 들어온 웹 애플리케이션의 컨텍스트 경로를 반환하는 메서드   

1. # response 객체   
   클라이언트의 응답 정보를 처리해주는 객체

1. # response 객체의 주요 메소드
   String getCharacterEncoding() : 한글 인토딩 형태를 구함   

   void addCookie(Cookie cookie) : 쿠키를 발행함   
   
   Void sendRedirect(String location) : 지정한 URL로 이동   

   
