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