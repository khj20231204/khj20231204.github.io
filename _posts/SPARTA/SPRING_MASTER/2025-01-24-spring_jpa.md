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

   ```java
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

1. # @GeneratedValue

   @GeneratedValue는 Java의 JPA(자바 지속성 API)에서 엔티티의 기본 키(primary key) 값을 자동으로 생성하기 위해 사용됩니다. 이 어노테이션은 주로 @Id와 함께 사용되며, 기본 키의 생성 전략을 정의합니다.   

   @GeneratedValue 옵션   

   | 옵션  |  설명  |
   |:-----:|:------:|
   | auto | 데이터베이스에 따라 기본키 생성 전략(default) |
   | identity | 데이터베이스가 자동으로 기본 키 값을 생성합니다(MySQL, SQL Server 등) |
   | sequence | 시퀀스를 사용하여 기본 키를 생성합니다.(Oracle, PostgreSQL 등) | 
   | table | 별도의 기본키 테이블을 이용해 기본키 생성 |

    ```java
      @Entity
      public class ExampleEntity {
      
         @Id
         @GeneratedValue(strategy = GenerationType.AUTO)
         private Long id;

         @Id
         @GeneratedValue(strategy = GenerationType.IDENTITY) // 전략 설정
         private Long id;

         @Id
         @GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "example_seq")
         @SequenceGenerator(name = "example_seq", sequenceName = "example_sequence", allocationSize = 1)
         private Long id;

         @Id
         @GeneratedValue(strategy = GenerationType.TABLE, generator = "table_gen")
         @TableGenerator(name = "table_gen", table = "id_table", pkColumnName = "id_name", valueColumnName = "id_value", allocationSize = 1)
         private Long id;

         ...
      }

   ```

1. # @SequenceGenerator()
   
   @SequenceGenerator의 필요성   
   데이터베이스의 시퀀스 이름 매핑   

   데이터베이스에서 사용하는 시퀀스 이름은 JPA에서 자동으로 추측되지 않습니다.
   @SequenceGenerator를 사용하여 JPA가 사용할 데이터베이스 시퀀스 이름(sequenceName)을 명시해야 합니다.
   기본값으로 설정하지 않으면 데이터베이스와 JPA 간에 시퀀스 이름 불일치로 오류가 발생할 수 있습니다.
   시퀀스의 고급 설정   
      
   @SequenceGenerator를 사용하면 시퀀스의 allocationSize, initialValue 등을 설정할 수 있습니다.
   예를 들어, 한 번에 여러 키 값을 미리 가져오거나 초기 값을 변경하는 등의 커스터마이징이 가능합니다.
   다중 시퀀스 사용   
      
   하나의 데이터베이스에서 여러 시퀀스를 사용하는 경우, 각 엔티티가 서로 다른 시퀀스를 참조하도록 설정할 수 있습니다.
   @SequenceGenerator로 시퀀스를 구분하여 필요한 설정을 각각 적용합니다.   

   ```java
      @Entity
      public class Customer {
         @Id
         @GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "customer_seq_gen")
         @SequenceGenerator(name = "customer_seq_gen", sequenceName = "customer_seq", allocationSize = 1)
         private Long id;

         private String name;
      }
   ```
   
   *@GeneratedValue(strategy = GenerationType.SEQUENCE)를 사용할 때 @SequenceGenerator가 필요한 이유는 시퀀스 생성의 세부 설정을 JPA에 알려주기 위함입니다. @SequenceGenerator를 생략할 경우, JPA는 기본 시퀀스 이름을 생성하여 사용합니다. 예를 들어, 엔티티 이름 뒤에 _SEQ를 붙여 **Customer_SEQ**라는 이름으로 시퀀스를 추측합니다. 하지만 데이터베이스에 기본적으로 해당 이름의 시퀀스가 없으면 오류가 발생합니다.   

   

   



