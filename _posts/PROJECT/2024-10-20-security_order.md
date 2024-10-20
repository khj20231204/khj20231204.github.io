---
layout: single
title: Security 실행 순서
categories: PROJECT
tag: []
author_profile: false
---   

1. # 실행 순서

   Initializing Servlet 'dispatcherServlet'   
   JwtRequestFilter.java의 doFilterInternal 메소드   
   JwtAuthenticationFilter.java 의  attemptAuthentication 메소드   
   CustomUserDetailService.java 의 loadUserByUsername 메소드   
   
 An internal error occurred while trying to authenticate the user.