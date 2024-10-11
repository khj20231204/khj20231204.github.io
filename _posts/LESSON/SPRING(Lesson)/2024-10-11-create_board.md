---
layout: single
title: 게시판 만들기
categories: SPRING(Lesson)
tag: []
author_profile: false
---

1. # 실습 개요
   spring 실습   

   프로젝트 명 : spring   

   계정생성   
   sqlplus system/oracle   

   create user spring identified by spring123;   
   grant connect, resource to spring;   

   ```javascript
      테이블명 : myboard  

      create table myboard(   
         no number primary key,
         writer varchar2(20),
         passwd varchar2(20),
         subject varchar2(50),
         content varchar2(100),
         readcount number,
         register date 
      );

      시퀀스 : myboard_seq
      create sequence myboard_seq
      start with 1
      increment by 1
      nocache;
   ```

   __java - myspring__   
   controller - BoardController.java   
   service - BoardService.java   
   dao - BoardDao.java   
   model - Board.java   

   __resources__   
   util - configuration.xml   
   sql - board.xml   

   __board__   
   boardform.jsp (글작성 폼)   
   boardlist.jsp (글목록)   
   boardcontent.jsp (상세 페이지)   
   boardupdateform.jsp (글수정 폼)   
   boarddeleteform.jsp (글삭제 폼)   

   __환경 설정 파일 작성 순서__   
   1) pom.xml   
   
   2) web.xml   
   ```xml
      <!-- 한글 인코딩 설정 : post방식 -->
      <filter>
         <filter-name>CharacterEncodingFilter</filter-name>
         <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
         <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
         </init-param>
         <init-param>
            <param-name>forceEncoding</param-name>
            <param-value>true</param-value>
         </init-param>
      </filter>
      <filter-mapping>
         <filter-name>CharacterEncodingFilter</filter-name>
         <url-pattern>/*</url-pattern>
      </filter-mapping>
   ```

   3) servlet-context.xml   
   3-1)webapp / index.jsp파일 생성
   ```
      <script>location.href = "test.do";</script>
      controller에 test.do 지정
   ```

      이후에
   ```javascript
      <context:component-scan base-package="com.myhome.spring" />
      =>
      <context:component-scan base-package="myspring" />
   ```
   base-package의 이름이 어떤 이름을 설정하냐에 따라 결정   
   com.myhome을 myspring으로 변경함   
   <img src="../../../imgs/LESSON/SPRING(Lesson)/myspring_path.png" style="border:3px solid black;border-radius:9px;width:300px">   

   4) configuration.xml   
   5) board.xml   
   6) root-context.xml 

   7)controller, service 생성   
   controller - BoardController.java   
   service - BoardService.java   

   8)dao 종류 설정해서 생성   
   1 - 클래스   
   2 - 인터페이스   

   9)Controller 작성   
   ```java
      @Controller
      public class BoardController {
         @Autowired
         private BoardService service;
      }
   ```   

   10)service 작성   
   ```java
      @Service
      public class BoardService {
         @Autowired
         private BoardDao dao;
      }
   ```

   11)

   12)webapp/board 폴더를 만들고 jsp파일 생성   

   13)configuration.xml 파일 생성 - mybatis 별칭 설정 파일   
   ```xml
      <?xml version="1.0" encoding="UTF-8" ?>
      <!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
      "http://mybatis.org/dtd/mybatis-3-config.dtd">

      <configuration>
         <typeAliases>
            <typeAlias alias="dept" type="myspring.model.Board" />
         </typeAliases>	
      </configuration>
   ```   
   이때 DTO클래스(Board)가 존재해야 Board를 설정할 수 있다   
   <img src="../../../imgs/LESSON/SPRING(Lesson)/configureation_setting.png" style="border:3px solid black;border-radius:9px;width:300px">   
  
  14)Board.xml   
  <img src="../../../imgs/LESSON/SPRING(Lesson)/board_setting.png" style="border:3px solid black;border-radius:9px;width:800px">   
         
   15)root-context.xml   
   ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xmlns:mybatis-spring="http://mybatis.org/schema/mybatis-spring"
         xsi:schemaLocation="http://mybatis.org/schema/mybatis-spring http://mybatis.org/schema/mybatis-spring-1.2.xsd
            http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.3.xsd">
         
         <bean id="hikariConfig" class="com.zaxxer.hikari.HikariConfig">
            <property name="driverClassName" value="oracle.jdbc.driver.OracleDriver"></property> 
            <property name="jdbcUrl" value="jdbc:oracle:thin:@localhost:1521:xe"></property>
            <property name="username" value="spring"></property> <!-- 수정 -->
            <property name="password" value="spring123"></property> <!-- 수정 -->
         </bean>

         <!-- HikariCP configuration -->
         <bean id="dataSource" class="com.zaxxer.hikari.HikariDataSource" destroy-method="close">
            <constructor-arg ref="hikariConfig" />
         </bean>

         <!-- 스프링으로 oracle db 연결 -->
         <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
            <property name="dataSource" ref="dataSource"></property>
            <property name="configLocation" value="classpath:util/configuration.xml" /> <!-- 경로 수정 -->
            <property name="mapperLocations" value="classpath:sql/*.xml" /> <!-- 파일 이름 수정 -->
         </bean>	
         
         <!-- mapper interface의  package설정 -->
         <mybatis-spring:scan base-package="myspring.dao"/><!-- 패키지명 수정 -->
      </beans>
   ```

1. # STS에 Data source Management 추가
   [Help] - Install New Software...   

   Add 버튼 클릭   

   Name :  DTP   
   Location : http://download.eclipse.org/datatools/1.14.1.201712071719/repository/   

   Contact all update sites during install to find required software 옵션 체크 해제   

