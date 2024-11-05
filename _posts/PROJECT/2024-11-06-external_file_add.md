---
layout: single
title: 외부에 파일 숨기고 값만 가져오는 설정
categories: PROJECT
tag: []
author_profile: false
---   

1. # 경로
   prop/JwtProps.java

   ```
      @Data
      @Component
      @ConfigurationProperties("com.hjcompany.server") //application.properties의 하위 속성 경로 지정
      public class JwtProps {
         
         //시크릿키 : JWT 시그니처 암호화를 위한 정보
         private String SecretKey;
      }
   ```

1. # configuratoinProperties 어노테이션이란
