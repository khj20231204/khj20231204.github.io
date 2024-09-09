---
layout: single
title: registerForm 설정
categories: SPRING
tag: []
author_profile: false
---

1. # 체크박스 값 서버로 전송
   registerForm.html   
   ```java
      <div class="sns-chk">
         <label><input type="checkbox" name="sns" value="facebook"/>페이스북</label>
         <label><input type="checkbox" name="sns" value="kakaotalk"/>카카오톡</label>
         <label><input type="checkbox" name="sns" value="instagram"/>인스타그램</label>
      </div>
   ```   

   registerForm.jsp   
   ```
      <h1>sns = ${param.sns}</h1>
   ```   

   체크박스에 name이 모두 sns로 같습니다. 페이스북과 카카오톡이 체크가 되어있다가정하고 url로 넘어갈 때를 보면   
   ```
      http://localhost/ch2/registerForm.jsp?sns=facebook$sns=kakakotalk
   ```   
   페이스북과 카카오톡이 sns 동일한 이름으로 넘어가기 때문에 서버에서 param.sns로 받는 값은 페이스북 1개가 됩니다.   

   다수의 값을 받을 경우 서버에서 param으로 받지 않습니다.   

   ParamValues란 메서드를 사용합니다.   

   ```js
      jsp: request.getParamValues("sns")

      el : ${paramValues.sns}
   ```   

   sns 다수 값 받기   
   1)el   
   ```java
      <h1>sns = ${paramValues.sns[0]}</h1>
      <h1>sns = ${paramValues.sns[1]}</h1>
      <h1>sns = ${paramValues.sns[2]}</h1>
   ```   

   2)jsp   
   ```jsp
      <% 
         String[] str = request.getParameterValues("sns"); 

         for(String s : str){
            %>
            <h1>sns=<%= s %></h1>	
            <%
         }	
      %>
   ```   

1. # `<c:url>`의 사용
   ```cs
      <form action="<c:url value="/register/save"/>" method="post" onSubmit="return formCheck(this)">
   ```   
   `<c:url>`이 하는 역할 2가지   
   1)context root 자동 추가   
   2)session id 자동 추가   


1. # 회원 가입 로딩 순서

   controller -> 회원가입폼.jsp -> controller -> 가입결과폼.jsp   

   1)회원가입 주소입력   
   ```cs
      //url주소
      localhost/ch4/register/add   
   ```   

   2)controller에서 받음   
   ```cs
      @RequestMapping("/register/add")   
      public String register(){
         return "registerForm"; //jsp파일의 회원가입 폼
      }   
   ```   

   3)registerForm.jsp   
   회원가입 폼 출력    
   form의 action주소를 controller주소로 입력   
   ```html
      <form action="/ch4/register/save" method=...>
   ```   

   4)controller에서 받음   
   ```cs
      @RequestMapping("/register/save")   
      public String register(){
         return "registerInfo";
      }      
   ```   

   5)registerInfo.jsp   
   회원가입 완료 결과 화면 출력   
   ```cs
      <%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

      <% 
         String[] str = request.getParameterValues("sns"); 

         for(String s : str){
            %>
            <h1>sns=<%= s %></h1>	
            <%
         }	
      %>

      <h1>id=${param.id}</h1>
      <h1>pwd=${param.pwd}</h1>
      <h1>name=${param.name}</h1>
      <h1>email=${param.email}</h1>
      <h1>birth=${param.birth}</h1>
   ```   
