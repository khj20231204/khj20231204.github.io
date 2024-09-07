---
layout: single
title: GetMapping와 PostMapping 빨간줄
categories: SPRING
tag: []
author_profile: false
---

1. # GetMapping와 PostMapping 빨간줄
   어노테이션을 추가해도 GetMapping과 PostMapping에 빨간줄이 생기는 경우가 있습니다.   

   <img src="../../imgs/spring/getmapping_error.png" style="border:3px solid black;border-radius:9px;width:400px">   
   다음과 같이 어노테이션에 GetMapping과 PostMappig 항목이 없는 것을 확인 할 수 있습니다.   

   pox.xml에서 springframework버전을 변경해 줍니다.   
    
   Spring Framework 5.x 버전 이상부터 JDK 11을 공식적으로 지원합니다

   ```cs
      <properties>
         <java-version>11</java-version>
         <org.springframework-version>5.2.25.RELEASE</org.springframework-version>
         <org.aspectj-version>1.6.10</org.aspectj-version>
         <org.slf4j-version>1.6.6</org.slf4j-version>
	   </properties>
   ```

   Spring Framework 버전 지원 문서입니다.   
   <a href="https://spring.io/projects/spring-framework#learn">https://spring.io/projects/spring-framework#learn</a>
