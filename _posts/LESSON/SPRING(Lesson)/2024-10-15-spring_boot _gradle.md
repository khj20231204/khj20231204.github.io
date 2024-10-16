---
layout: single
title: sbboard01
categories: SPRING(Lesson)
tag: []
author_profile: false
---
 
1. # 프로젝트 생성

   pom.xml파일 dependency 추가   
   ctrl + shift + f : 자동 정렬 기능   

   ```xml
      <!-- 내장 Tomcat실행시 jsp 파일을 사용하기 위한 의존 라이브러리 -->
		<dependency>
			<groupId>org.apache.tomcat.embed</groupId>
			<artifactId>tomcat-embed-jasper</artifactId>
			<scope>provided</scope>
		</dependency>
		<!-- jstl -->
		<dependency>
			<groupId>org.glassfish.web</groupId>
			<artifactId>jakarta.servlet.jsp.jstl</artifactId>
			<version>3.0.0</version>
		</dependency>
   ```

1. # application.properties 설정
   

