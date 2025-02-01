---
layout: single
title: JPA 쿼리 메소드드
categories: SPRING_MASTER
tag: []
author_profile: false
---
 
1. # 🔍 Spring Data JPA Query Methods 정리
   Spring Data JPA는 메서드 이름을 기반으로 자동으로 쿼리를 생성하는 Query Method 기능을 제공합니다.   
   즉, findBy, countBy, existsBy 같은 키워드를 사용하여 직접 쿼리를 작성하지 않아도 자동으로 SQL을 실행할 수 있습니다.   


1. # findBy (조회)
   특정 필드 값을 기준으로 데이터를 조회   
   ```java
      User findByUsername(String username);
      User findByEmail(String email);
      Optional<User> findById(Long id);
   ```   
   ✔ Optional<>을 사용하면 null 방지 가능   

1. # countBy (개수 조회)
   특정 조건을 만족하는 데이터 개수 조회   
   ```java
      Long countByRole(String role);
      Long countByStatus(String status);
   ```

1. # existsBy (존재 여부 확인)
   특정 값이 존재하는지 확인 (boolean 반환)   
   ```java
      boolean existsByUsername(String username);
      boolean existsByEmail(String email);
   ```

1. # deleteBy (삭제)
   특정 조건을 만족하는 데이터 삭제   
   ```java
      void deleteByUsername(String username);
      void deleteByEmail(String email);
   ```

1. # AND, OR 조건
   1️⃣ And (여러 조건 AND)   
   ```java
      User findByUsernameAndEmail(String username, String email);
      User findByFirstNameAndLastName(String firstName, String lastName);
   ```   
   ✔ AND 연산자로 두 개의 필드가 모두 일치하는 데이터 검색   

   2️⃣ Or (여러 조건 OR)   
   ```java
      List<User> findByUsernameOrEmail(String username, String email);
      List<User> findByFirstNameOrLastName(String firstName, String lastName);
   ```
   ✔ OR 연산자로 둘 중 하나라도 일치하면 검색   

1. # 비교 연산자 (GreaterThan, LessThan 등)
   
   GreaterThan :	초과 (>)   
   GreaterThanEqual : 이상 (>=)   
   LessThan	: 미만 (<)   
   LessThanEqual : 이하 (<=)   
   ```java
      List<User> findByAgeGreaterThan(int age);  // age > ?
      List<User> findByAgeLessThanEqual(int age);  // age <= ?
   ```

1. # LIKE 검색 (문자열 패턴)
   Like : 부분 일치 (%값%)   
   NotLike : 부분 불일치 (NOT LIKE)   
   StartingWith : 접두사 검색 (값%)   
   EndingWith : 접미사 검색 (%값)   
   Containing : 포함 여부 (%값%과 동일)   
   
   ```java
      List<User> findByUsernameLike(String username);  // '%username%'
      List<User> findByEmailContaining(String email);  // '%email%'
      List<User> findByFirstNameStartingWith(String prefix);  // 'prefix%'
      List<User> findByLastNameEndingWith(String suffix);  // '%suffix'
   ```

1. # 정렬 및 페이징
   📌 1️⃣ 정렬 (OrderBy)   
   ```java
      List<User> findByRoleOrderByUsernameAsc(String role); // role 기준 검색 후 username 오름차순 정렬
      List<User> findByAgeOrderByUsernameDesc(int age); // age 기준 검색 후 username 내림차순 정렬
   ```

   📌 2️⃣ 페이징 (Pageable)   
   ```java
      Page<User> findByRole(String role, Pageable pageable);
      Slice<User> findByAgeGreaterThan(int age, Pageable pageable);
   ```
   ✔ Page와 Slice를 사용하면 페이징 처리 가능

   ```java
      Pageable pageable = PageRequest.of(0, 10, Sort.by("username").ascending());
      Page<User> users = userRepository.findByRole("USER", pageable);
   ```
   ✔ 0번 페이지에서 10개 가져오고, username 기준 오름차순 정렬   

1. # @Query로 직접 쿼리 작성
   Query Method로 해결하기 어려운 복잡한 쿼리는 @Query를 사용하여 직접 작성 가능   

   📌 1️⃣ JPQL 사용   
   ```java
      @Query("SELECT u FROM User u WHERE u.username = :username")
      User findByUsernameCustom(@Param("username") String username);
   ```

   📌 2️⃣ 네이티브 SQL 사용   
   ```java
      @Query(value = "SELECT * FROM user WHERE email = :email", nativeQuery = true)
      User findByEmailNative(@Param("email") String email);
   ```

1. # 결론 (핵심 요약)
   ✔ findBy → 특정 필드 값으로 검색   
   ✔ countBy → 개수 조회   
   ✔ existsBy → 존재 여부 확인 (boolean)   
   ✔ deleteBy → 특정 조건 데이터 삭제   
   ✔ And, Or → 다중 조건 검색   
   ✔ GreaterThan, LessThan → 비교 연산자   
   ✔ Like, Containing, StartingWith → 문자열 검색   
   ✔ OrderBy → 정렬   
   ✔ Pageable → 페이징 처리 가능   
   ✔ @Query → JPQL 또는 네이티브 SQL 직접 작성 가능   
