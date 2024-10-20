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
 
   1. 클라이언트 요청: 클라이언트가 인증된 상태로 시스템의 자원에 접근하려고 요청을 보냅니다.   
   1. Initializing Servlet 'dispatcherServlet'   
   1. JwtRequestFilter   
   1. JwtAuthenticationFilter 실행: 요청이 들어오면 스프링 시큐리티 필터 체인에서 JwtAuthenticationFilter가 가장 먼저 실행됩니다.   
   1. JWT 토큰 검증: JwtAuthenticationFilter는 요청 헤더에서 JWT 토큰을 추출하고 유효성을 검증합니다.
   1. 토큰 유효성 확인   

      유효한 경우:   
      1. Authentication 객체를 생성하여 SecurityContext에 설정하고, 후속 요청에 대한 권한 검사를 진행합니다.   
      
      유효하지 않은 경우:   
      1. UserDetailsService를 호출하여 사용자 정보를 다시 조회하고, 새로운 토큰을 발급하는 등의 처리를 수행합니다.   
      1. UserDetailsService 실행 (필요한 경우): JwtAuthenticationFilter에서 토큰 검증에 실패하거나, 새로운 토큰을 발급해야 할 경우 UserDetailsService가 호출되어 사용자 정보를 조회하고 UserDetails 객체를 생성합니다.   
