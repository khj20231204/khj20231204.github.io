---
layout: single
title: 컨트롤러에서 jsp로 값 전달
categories: SPRING
tag: []
author_profile: false
---

1. # redirect
   ```java
      @PostMapping("/register/save")
      public String save(User user, Model m) throws Exception{
         
         if(!isValid(user)) {
            String msg = URLEncoder.encode("id를 잘못 입력", "utf-8") ;
            
            return "redirect:/register/add?msg="+msg; //url재작성(rewriting)
         }
         return "registerInfo";
      }
   ```   

   /register/add.jsp 파일   
   ```html
      <%@ page import="java.net.URLDecoder" %>

      <div id="msg">${param.msg}</div> <!-- 이렇게 해서 msg가 안보이는 경우 -->
      <div id="msg">${URLDecoder.decode(param.msg, "utf-8")}</div> <!-- decoding을 해준다 -->
   ```   

1. # Model
   ```java
      @PostMapping("/register/save")
      public String save(User user, Model m) throws Exception{
         
         if(!isValid(user)) {
            String msg = URLEncoder.encode("id를 잘못 입력", "utf-8") ;
            m.addAttribute("msg",msg);
            return "redirect:/register/add"; //url재작성(rewriting)
         }
         return "registerInfo";
      }
   ```   
   return "redirect:/register/add?msg="+msg; 이거 한줄이   

   밑에 2줄과 같습니다.   

   m.addAttribute("msg",msg);   
   return "redirect:/register/add";   

   get방식으로 redirect를 보내면 받는 jsp에서 param으로 값을 받을 수 있습니다.   
   model에 넣으면 redirect로 주소만 보내도 받는 jsp에서 param으로 값을 받을 수 있습니다.   

1. #  param대신 클래스
   컨트롤러에서 넘겨주는 값   
   ```java
      @PostMapping("/register/save")
      public String save(User user, Model m) throws Exception{
         
         if(!isValid(user)) {
            String msg = URLEncoder.encode("id를 잘못 입력", "utf-8") ;
            m.addAttribute("msg", msg);
            return "redirect:/register/add";
         }
         return "registerInfo";
      }
   ```   

   JSP에서 받는 값   
   ```jsp
      <%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>

      <% 
         String[] str = request.getParameterValues("sns"); 

         for(String s : str){
            %>
            <h1>sns=<%= s %></h1>	
            <%
         }	
      %>

      <h1>id=${user.id}</h1>
      <h1>pwd=${user.pwd}</h1>
      <h1>name=${user.name}</h1>
      <h1>email=${param.email}</h1>
      <h1>birth=${param.birth}</h1>
      <h1>sns=${param.sns}</h1>
   ```   
   넘겨받은 클래스user로도 값을 전달 받을 수 있고, param으로도 값을 받을 수 있습니다.   
