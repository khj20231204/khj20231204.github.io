---
layout: single
title: 서블릿과 JSP
categories: SPRING
tag: []
author_profile: false
---

1. # 

1. # JSP의 호출
    twoDice.jsp요청이 들어온다.   

    확장자가 jsp인 파일이 들어오면 JspServlet이 모두(*.jsp) 받아서 서블릿 인스턴스의 존재를 파악한다.   

    twoDice.jsp로 만든 서블릿이 없는 경우 twoDice.jsp를 서브릿 소스파일로 변환한다.   
    ex)twoDice.jsp => twoDice.java   

    서블릿 파일로 변환 후 컴파일해서 class파일을 만든다.   
    ex)twoDice.java => twoDice.class   

    twoDice.java를 이용해서 객체를 생성한다. 이때 jspInit() 메소드 호출   

    서블릿 인스턴스에서 요청처리 jspService()   

    init()는 초기화, Service()는 요청처리   

    : 최초 호출 시에만 변환 후 객체 생성까지 지연시간이 있고, 이후부터는 바로 객체로 간다

1. # JSP의 기본 객체
    ```jsp
        <%@ page contentType="text/html;charset=utf-8"%>
        <%@ page import="java.util.Calendar" %>
        <%
            String year  = request.getParameter("year");
        %>
    ```   
    request.getParameter는 객체 생성없이 바로 사용된다. JSP자체에서 기본 객체를 제공하기 때문이다.  