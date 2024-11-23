---
layout: single
title: JWT와 간단한 진행 과정
categories: PROJECT
tag: []
author_profile: false
---   

1. # JWT란
   JWT (JSON Web Token)는 웹에서 사용자 인증과 정보 교환을 안전하게 처리하기 위해 사용되는 JSON 형식의 토큰입니다. JWT는 세 가지 주요 부분으로 구성됩니다   

   1)헤더 (Header): 토큰의 타입(예: JWT)과 서명 알고리즘(예: HMAC SHA256 또는 RSA)을 지정합니다.   
   2)페이로드 (Payload): 토큰에 담을 데이터가 포함된 부분입니다. 이 데이터는 주로 사용자 정보(예: 사용자 ID)나 서버에서 사용될 정보를 포함합니다. 그러나 JWT는 암호화되지 않기 때문에 민감한 데이터는 저장하지 않는 것이 좋습니다.   
   3)서명 (Signature): 헤더와 페이로드를 비밀 키나 공개/개인 키 쌍을 사용해 서명한 부분입니다. 이를 통해 토큰의 무결성을 확인하고, 변조 여부를 검증할 수 있습니다.   
   
   인증 (Authentication): 사용자가 로그인하면 서버에서 JWT를 생성해 사용자에게 전달하고, 이후 사용자는 이 토큰을 서버에 제출하여 인증을 받습니다.   

   정보 교환 (Information Exchange): JWT는 정보를 안전하게 교환할 수 있는 방법을 제공합니다. 토큰의 서명 덕분에 데이터를 변조할 수 없습니다.   

   JWT는 주로 RESTful API나 웹 애플리케이션에서 인증 시스템에 사용되며, 그 자체로 간단하고 효율적입니다.   

1. # JWT 전송 과정

   1)사용자가 최초 로그인 시 아이디와 비밀번호를 입력 후 로그인 요청   
   2)서버에서 사용자의 아이디와 비밀번호를 확인, 이때 비밀번호는 서버에 해쉬로 저장되어 있는 상태   
   3)아이디와 비밀번호가 일치하면 서버에서 토큰 생성   
   4)토큰 생성 과정은 따로 설명 -------------   
   5)비밀키는 서버가 가지고 있고, 토큰(헤더, 페이로드, 서명을 암호화한 결과물)을 클라이언트에게 전송   
   6)이후 클라이언트의 재접속이나 보호된 자원에 접근 하는 등 요청이 이루어지면 서버에서 클라이언트의 토큰 정보를 가지고 인증 절차를 거침   
   7)인증 절차는 따로 설명 ------------------   

1. # 간단한 진행 과정

   Initializing Servlet 'dispatcherServlet'   
   JwtRequestFilter.java의 doFilterInternal 메소드   
   JwtAuthenticationFilter.java의 attemptAuthentication 메소드   
   CustomUserDetailService.java의 loadUserByUsername 메소드   
 
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

1. # 인증 관련 절차
   
   __회원가입__ : 인증과정 X   
   아직 인증된 사용자가 아니기 때문에, JWT를 이용한 인증 과정을 거치지 않습니다. 일반적으로 회원가입 요청은 인증이 필요하지 않은 요청이므로, 인증 관련 필터(예: UsernamePasswordAuthenticationFilter, JwtAuthenticationFilter)는 건너뛰게 됩니다.   

   __로그인__ : 인증과정 O   
   아이디와 패스워드 사용   

   인증을 성공하면 -> 토큰 생성   

   토큰 검증   