---
layout: single
title: JPA
categories: SPRING_MASTER
tag: []
author_profile: false
---
 
1. # 객체와 테이블 매핑
   도메인 객체를 관계형 데이터베이스 테이블로 맵핑할 때 @Entity 어노테이션을 사용합니다.   
   @Entity 어노테이션만 선언했을 때 __클래스 이름이 테이블 이름__ 이 되고 대/소문자 치환은 일어나지 않습니다.   
   대부분의 RDBMS는 대/소문자를 가리지 않으므로 기본 JPA 작명규칙이 문제되지 않습니다.   
   @Table 어노테이션을 사용해서 테이블 이름을 명시적으로 표기할 수 있습니다.   

   ```java
      @Entity
      public class User{
         ...
         String userId;
         String userName;
         String email;
         ...
      }

      @Entity
      public class Seller extends User{
         ...
      }

      @Entity
      public class Buyer extends User{
         ...
      }
   ```   

1. # @Entity
   @Entity 어노테이션을 붙이면 영속 객체로 관리가 되는데 이때 기본 생성자는 반드시 필요합니다.   
   final, interface, innder class, 열거형는 영속 객체가 될 수 없음   
   영속 객체 필드에는 final을 사용할 수 없음 => 해당 필드가 set으로 정의될 수 있어야 update가능      

1. # @Table
   관습적인 테이블 서계 방법에서 테이블 이름은 대문자에 "_"를 사용할 수 있습니다.   
   @Table 어노테이션은 스키마를 지정하거나 테이블 이름을 구체적으로 명시합니다.   
   특정 RDBMS는 스키마 지정을 테이블 이름에 포함할 수 있기에 "SA.USER"로 스키마 지정이 가능합니다.   
   @Table(name="USER", catalog="CATALOG")로 카탈로그 지정이 가능합니다.   

   @Table 옵션   
   
   |   옵션  |   설명 |
   |:------:|:------:|
   | name | 매핑한 테이블 이름 지정(기본 : 클래스명) |
   | catalog | 데이터베이스 catalog 매핑(catalog 기능이 있는 경우) |
   | schema | 데이터베이스 schema 매핑(schema 기능이 있는 경우) |
   | uniqueConstraints | DDL생성에서 unique 제약 조건 생성(자동 생성 기능시) |

   스키마 자동생성 옵션   
   ```
      <property name="hibernate.hbm2ddl.auto" value="create"/>
   ```   

1. # @Access
   JPA에서 객체에 대한 접근 방식은 크게 필드 접근 방법과 프로퍼티 접근 방법이 있습니다.   
   @Access를 적용하지 않을 경우 @Id 어노테이션의 지정 위치에 따라 접근 방법을 결정할 수 있습니다.   
   @Access 어노테이션을 선언해서 명시적으로 접근 방법을 설정할 수 있습니다.   
   @Access 어노테이션으로 필드/속성 접근 방법을 동시에 사용할 수도 있습니다.   

1. # Id   
   @Id   
   @IdClass - 복합키와 관련      
   @EmbeddedId - 복합키와 관련   

   피해야 할 타입 : float, Float, double 등을 피해야 합니다. Timestamp 타입을 피해야 합니다.   

   ```
      @Entity
      public class Catagory{
 
         @Id
         protected Long id;

         public Long getId(){
            return this.id;
         }

         public void setId(Long id){
            this.id = id;
         }
      }
   ```

   

   



