---
layout: single
title: mybatis용어
categories: SPRINGBOOT
tag: []
author_profile: false
---

1. # mapper 용어

   데이터베이스 컬럼 이름과 Java 객체의 프로퍼티 이름이 다를 경우 resultMap을 사용하여 매핑.   

   ```xml
      <!-- ⓐ -->
      <resultMap type="Users" id="userMap">  

         <!-- ⓑ -->
         <id property="no" column="no" />
         
         <!-- ⓒ -->
        <result property="userId" column="user_id" />
        <result property="userPw" column="user_pw" />

         <!-- ⓓ -->
         <collection property="authList" resultMap="authMap"></collection>

      </resultMap>

      <!-- UserAuth 매핑 -->
      <!-- ⓔ -->
      <resultMap type="UserAuth" id="authMap">
         <result property="userId" column="user_id" />
         <result property="auth" column="auth" />
      </resultMap>

      <!-- ⓕ -->
      <select id="getUserById" parameterType="int" resultMap="userMap">
   ```

   `ⓐ <resultMap type="Users" id="userMap">` : Mybatis에서 SQL 쿼리 결과를 Java 객체로 변환하기 위해 사용하는 설정 요소입니다. `<resultMap>` 로 둘러싸인 `<result>` 값에서   
   ```
      컬럼명 : user_id → 자바변수 : userId 로 변환 
      컬럼명 : user_pw → 자바변수 :userPw 로 변환
   ```
   스테이크 case의 컬럼명을 파스칼 case의 변수명으로 변환.   
   Users란 클래스는 필드로 userId, auth를 가진다.   
   Users 클래스를 맵핑하는 resultMap이름은 userMap.   

   type : 클래스 Users 에 맞춰서 맵핑   
   id="userMap" : 이 맵핑을 userMap의 이름으로 사용   

   `ⓑ <id property="no" column="no" />` : id는 주로 PK값에 부여, 고유한 값을 나타냄   

   `ⓒ <result property="userId" column="user_id" />` : user_id → userId로 변환   

   `ⓓ <collection property="authList" resultMap="authMap"></collection>` : List, Map, Array 같은 collection은 맵핑.   
   reusltMap으로 authMap을 사용하면 "autList"로 변환   

   `ⓔ <resultMap type="UserAuth" id="authMap">` : UserAuth클래스를 맵핑하는 reusltMap의 이름은 authMap   

   `ⓕ <select id="getUserById" parameterType="int" resultMap="userMap">` : resultMap="userMap"**을 통해 조회 결과를 userMap에 정의된 규칙에 따라 Users객체로 변환합니다.   

   