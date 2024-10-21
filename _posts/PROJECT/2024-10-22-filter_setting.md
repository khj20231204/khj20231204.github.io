---
layout: single
title: 필터 설정
categories: PROJECT
tag: []
author_profile: false
---   

1. # 필터 설정

   설정 예)   
   ```java
      http.addFilterAt(new JwtAuthenticationFilter(authenticationManager, jwtTokenProvider), UsernamePasswordAuthenticationFilter.class)
      .addFilterBefore(new JwtRequestFilter(authenticationManager, jwtTokenProvider),UsernamePasswordAuthenticationFilter.class);
   ```
   JwtAuthenticationFilter :  인증 성공 시 JWT 토큰을 생성하고 클라이언트에게 전달합니다.   
   *JwtAuthenticationFilter는 UsernamePasswordAuthenticationFilter을 상속받습니다.   
   *UsernamePasswordAuthenticationFilter : 로그인 요청이 들어왔을 때 가장 먼저 실행되는 인증 필터로 JWT 기반 인증을 수행   


   JwtAuthenticationFilter: 로그인 할 때만 __인증(아이디와 비밀번호)__ 과 __토큰 생성__ 담당   
   JwtRequestFilter: 모든 요청에 대해 JWT 토큰을 검증하는 역할을 수행하여 일관된 인증 방식을 유지합니다.   

   -SecurityConfig.java-   
   ```java
      //필터 설정
      http.addFilterAt(new JwtAuthenticationFilter(authenticationManager, jwtTokenProvider), UsernamePasswordAuthenticationFilter.class).addFilterBefore(new JwtRequestFilter(authenticationManager, jwtTokenProvider),UsernamePasswordAuthenticationFilter.class);
   ```
