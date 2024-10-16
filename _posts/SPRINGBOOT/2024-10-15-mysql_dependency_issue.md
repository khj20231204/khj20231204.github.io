---
layout: single
title: 스프링 부트에서 mysql dependency 문제
categories: SPRINGBOOT
tag: []
---

1. # 버전 유무

   버전이 없으면 error발생
   ```
      implementation 'mysql:mysql-connector-java'
   ```

   버전이 있으면 정상 작동
   ```
      implementation 'mysql:mysql-connector-java:8.0.33'
   ```

   하지만, 어느 경우는 버전이 없어도 정상작동 하는 이유?   

   pring Boot에서 mysql:mysql-connector-java 같은 의존성을 추가할 때 버전을 명시하지 않고 사용할 수 있는 이유는 Spring Boot의 Dependency Management 기능 때문입니다. io.spring.dependency-management Gradle 플러그인 또는 Maven을 사용할 때 spring-boot-starter-parent를 부모 POM으로 사용하면, 스프링 부트에서 “축복받은(blessed)” 의존성에 대해 자동으로 관리되는 버전을 적용해줍니다.   
      
   이 경우에는 version 태그를 생략할 수 있으며, 이 기능을 사용하기 위해서는 org.springframework.boot Gradle 플러그인이 적용되어 있어야 합니다. 그러나, 플러그인을 적용하지 않은 경우나 버전 관리되는 의존성이 아닌 경우에는 직접 버전을 명시해주어야 합니다.   

