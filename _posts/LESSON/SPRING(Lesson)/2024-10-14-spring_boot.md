---
layout: single
title: Spring Boot
categories: SPRING(Lesson)
tag: []
author_profile: false
---

1. # Spring Boot
   
   war : 배포시 아파치 톰캣 외부서버가 필요   
   jar : 내장 톰캣으로 실행   

   Dynamic web module 버전은 톰캣에 의해 결정   
   톰캣 10.1 => Dynamic web moudle : 6.0   

   gradle : build.gradle 이 자동 생성되며 이 파일이 gradle 설정 파일   
   maven : pom.xml이 자동 생성되면 이 파일이 maven 설정 파일   

   resources/static : 공유폴더, 이미지나 txt파일등을 저장

   templates : thymeleaf를 사용할 때 html파일을 전부 templates에 저장   
   *단, thymeleaf 설정이 되어있어야 한다.   
   thymeleaf vs jstl   

   application.properties : 환경 설정 파일   
   포트, db 설정 등을 입력   

   webapp : jsp파일

1. # 외부 톰캣에서 실행
   내장 톰캣 : http://localhost:8005/
   외장 톰캣 : http://localhost/demo/
