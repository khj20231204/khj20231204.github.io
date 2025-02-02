---
layout: single
title: dependency
categories: SPRING_MASTER
tag: []
author_profile: false
---
 
1. # 의존성 구성
   dependencies 블록 내에서 implementation, compileOnly, runtimeOnly 같은 키워드들은 의존성 구성(Configuration) 이라고 부릅니다. Gradle에서는 의존성을 어떻게 포함하고 사용할지를 결정하는 여러 가지 의존성 구성이 있습니다.   

1. #  implementation 
   __컴파일__ 및 __런타임__ 에 포함되는 의존성   
   해당 라이브러리를 사용하는 코드가 있으면 컴파일 시 필요하고, 실행 시에도 필요함.   
   가장 일반적으로 사용하는 의존성.   

   ```java
      dependencies {
         implementation 'org.springframework.boot:spring-boot-starter-web'
      }
   ```

1. # compileOnly
   컴파일 시에만 필요한 의존성 (런타임에서는 제외됨)   
   예를 들어, 애플리케이션에서 특정 인터페이스만 사용하지만, 실제 실행할 때는 다른 곳에서 구현체를 주입하는 경우에 사용함.   
   Lombok 같은 어노테이션 프로세서가 대표적인 예.   
   
   ```java
      dependencies {
         compileOnly 'org.projectlombok:lombok:1.18.22'
      }
   ```

1. # runtimeOnly
   컴파일할 때는 필요 없지만, 실행할 때만 필요한 의존성   
   예를 들어 JDBC 드라이버 같은 것이 대표적임.   
   인터페이스만 사용하고, 실제 실행할 때 구현체를 주입하는 경우.   

   ```java
      dependencies {
         runtimeOnly 'mysql:mysql-connector-java:8.0.33'
      }
   ```   

1. # testImplementation
   테스트 코드에서만 사용하는 의존성   
   애플리케이션의 실제 코드에는 영향을 주지 않고, 테스트 코드에서만 동작함.   
   JUnit, Mockito 같은 라이브러리를 포함할 때 사용됨.   

   ```java
      dependencies {
         testImplementation 'org.junit.jupiter:junit-jupiter-api:5.9.0'
      }
   ```

1. # testCompileOnly
   테스트 코드의 컴파일 시에만 필요한 의존성   
   테스트를 실행할 때는 필요하지 않음.   
   잘 사용되지 않는 의존성 구성   

1. # testRuntimeOnly
   테스트 실행 시에만 필요한 의존성   
   컴파일할 때는 필요하지 않지만, 테스트를 실행할 때 필요한 경우 사용.   

   ```java
      dependencies {
         testRuntimeOnly 'org.junit.jupiter:junit-jupiter-engine:5.9.0'
      }
   ```




