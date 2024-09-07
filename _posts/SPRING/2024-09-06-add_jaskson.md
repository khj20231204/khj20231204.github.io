---
layout: single
title: Jackson Databind 설치
categories: SPRING
tag: []
author_profile: false
---

1. # Jackson Databind
   구글에서 maven repository를 검색 → jackson 검색 → jackson Databind   
   
   또는   

   <a href="https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind">
   https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind</a>    
   
   Jackson Databind 2.9.0 이상 버전부터 JDK 11을 공식적으로 지원합니다. 하지만 최신 버전을 받는 것은 권장합니다.   

   2.17.2 버전 선택 → Maven탭에서   

   ```
      <dependency>
         <groupId>com.fasterxml.jackson.core</groupId>
         <artifactId>jackson-databind</artifactId>
         <version>2.17.2</version>
      </dependency>
   ```   
   복사 후 pom.xml의 dependency에 추가   

   프로젝트 오른쪽 마우스 → Maven → Update Project → 서버 재시작   
