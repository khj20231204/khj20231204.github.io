---
layout: single
title: JPA 영속성과 어노테이션
categories: JPA
tag: []
author_profile: false
--- 

1. # 영속성
   사전적 의미는 영원이 계속되는 성질이나 능력을 말합니다.   
   어플리케이션의 상태와 상관 없도록 물리적 저장소를 이용해 데이터를 저장하는 행위를 영속화(≒ DB에 저장하는 것)라 할 수 있습니다.   
   데이터를 어떤 공간에 어떤 형태로 저장할 것인가에 따라 영속화 방식은 달라집니다.   

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

1. # @Id
   데이터베이스 PK와 매핑   

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
         @GeneratedValue(strategy = GenerationType.IDENTITY) // MySQL, h2
         private Long id;

         @Id
         @GeneratedValue(strategy = GenerationType.SEQUENCE) //Oracle, PostgreSQL
         private Long id;

         @Id
         @GeneratedValue(strategy = GenerationType.TABLE, generator = "table_gen")
         @TableGenerator(name = "table_gen", table = "id_table", pkColumnName = "id_name", valueColumnName = "id_value", allocationSize = 1)
         private Long id;

         ...
      }
   ```   

   GenerationType.SEQUENCE을 커스터마이징하기 위해서는 @SequenceGenerator를 사용   
   GenerationType.TABLE을 커스터마이징이하기 위해서는 @TableGenerator를 사용   
   GenerationType.IDENTITY를 커스터마이징하기 위한 어노테이션을 따로 존재하지 않음   

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
         @GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "customer_seq_gen") //generator와 @SequenceGenerator의 name가 일치해야한다
         @SequenceGenerator(name = "customer_seq_gen", sequenceName = "customer_seq",initialValue = 1, allocationSize = 1) //sequenceName이 DB의 sqeunce 이름이된다
         private Long id;

         private String name;
      }
   ```
   
   *@GeneratedValue(strategy = GenerationType.SEQUENCE)를 사용할 때 @SequenceGenerator가 필요한 이유는 시퀀스 생성의 세부 설정을 JPA에 알려주기 위함입니다. @SequenceGenerator를 생략할 경우, JPA는 기본 시퀀스 이름을 생성하여 사용합니다. 예를 들어, 엔티티 이름 뒤에 _SEQ를 붙여 **Customer_SEQ**라는 이름으로 시퀀스를 추측합니다. 하지만 데이터베이스에 기본적으로 해당 이름의 시퀀스가 없으면 오류가 발생합니다.   
   @GeneratedValue의 generator 설정값과 @SequenceGenerator의 name이 일치해야합니다.   
   @SequenceGenerator의 sequenceName이 DB의 sequence명이 됩니다.   

   initialValue : 초기 시작값   
   allocationSize : 한번에 메모리에 불러올 수 있는 크기, allocationSize = 1이면 JPA는 매번 ID를 생성할 때마다 데이터베이스 시퀀스를 호출합니다. 하지만 allocationSize = 50으로 설정하면 한 번에 50개의 ID를 미리 가져와 메모리에 캐싱하고, 이후 ID 생성 요청에서는 데이터베이스에 접근하지 않고도 처리합니다.   


1. # @TableGenerator   

   1.기본키 생성을 위해 별도의 테이블을 생성하고 이 테이블을 이용해 기본키를 생성합니다.   
   2.Table 기본키 생성 전략은 별도의 테이블을 생성하기 때문에 데이터베이스 종류에 영향을 받지 않습니다.   
   3.Table 생성 전략을 적용하기 위해서는 @TableGenerator 어노테이션이 필요하며 여러 옵션을 적용할 수 있습니다.   
   4.Table 생성 전략은 테이블 생성과 키값 증가를 위한 update가 실행되기 때문에 성능에 대한 고려가 필요합니다.   

   *@SequenceGenerator와 @TableGenerator는 명시적인 설정을 통해 전략을 커스터마이징하거나 기본값을 대체하는 데 사용됩니다.  

   ```java  
     @Entity
     @Table(name="customer_tb")
     @TableGenerator(name="id_generator", table="customer_tb", pkColumnName="id_name", pkColumnValue="customer_id", valueColumnName="next_value", initialValue=0, allocationSize=1)
     public class Customer{

         @Id
         @GeneratorValue(strategy=GenerationType.TABLE, generator="id_generator")
         private Long id;
         ...
     }
   ```   

   | 속성  |  기능 |  기본값 |
   |:-----:|:-----:|:-----:|
   | name |식별자 생성기 이름|필수|
   | table |키생성 테이블명|hibernate_sequences|
   |pkColumnName|시퀀스 컬럼명|sequence_name|
   |valueColumnName|시퀀스 값 컬럼명|next_val|
   |pkColumnValue|키로 사용할 값 이름|엔티티 이름|
   |initialValue|초기 값, 마지막으로 생성된 값이 기준이다.|0|
   |allocationSize|시퀀스 한 번 호출에 증가하는 수(성능 최적화에 사용)|50|
   |catalog,schema|데이터베이스 catalog, schema 이름||
   |uniqueConstraints|유니크 제약 조건을 지정할 수 있다||


1. # @Column
   @Column 어노테이션은 영속 객체의 필드와 데이터베이스 테이블의 열(column)을 매핑할 때 사용합니다.   
   @Columnn 어노테이션은 당야한 옵션 기능을 제공하며 이를 통해 영속 객체 필드의 속성을 정의할 수 있습니다.   
   @Column의 여러 속성들은 대부분 선택적으로 사용하며 기본값이 지정되어 있습니다.   

   |  옵션  |  설명  |
   |:------:|:------:|
   | name | 해당 테이블 열의 이름을 지정 |
   | nullable | NULL 값 허용 여부(default:true) |
   | unique | Unique 제약 조건 여부(default:false) |
   | length | 문자(String)의 길이 지정(default:255) |
   | precision | 숫자의 전체 자릿수 지정 |
   | scale | 소수점 이하 자릿수 지정 |
   | insertable | 엔티티가 저장될 때 컬럼이 저장될지 여부(default:true) |
   | updatable | 엔티티가 수정될 때 컬럼이 수정될지 여부(default:true)|
   | table | 컬럼이 속한 테이블 지정 |
   | columnDefinition | 컬럼에 대한 정의를 직접 지정 |

   ```java
      @Entity
      @Table(name="USERS")
      public class User{
         @Id
         @Column(name="USER_ID", nullable=false)
         private Long userId;
         
         @Column(name="USER_NAME", nullable=false)
         private String username;

         @Column(name="FIRST_NAME", nullable=false, length=1)
         private String firstName;

         @Column(name="LAST_NAME", nullable=false)
         private String lastName;
      }
   ```   

1. # @Temporal
   @Temporal 어노테이션은 영속 객체의 날짜 및 시간 필드에 적용합니다.   
   자바의 날짜 및 시간 정보는 년,월,일과 시,분,초를 하나의 필드로 표현할 수 있지만 데이터베이스에 따라 날짜, 시간, 날짜와 시간 컬럼의 타입이 다르기 대문에 이를 @Temporal 어노테이션으로 지정할 수 있습니다.   
   
   | 옵션 | 기능 |
   |:----:|:----:|
   |TemporalType.DATE|날짜(년, 월, 일)|
   |TemporalType.TIME|시간(시, 분, 초)|
   |TemporalType.TIMESTAMP|날짜와 시간|
      
   ```java

      @Entity
      @Table(name="USER")
      public class User{

         @Id
         @Column(name="USER_ID", nullable=false)
         private Long userId;

         @Temporal(TemporalType.DATE)
         private Date mydate; //날짜

         @Temporal(TemporalType.TIME)
         private Date mytime; //시간

         @Temporal(TemporalType.TIMESTAMP)
         private Date mytimestamp; //날짜와 시간
      }

      -- 생성된 DDL --
      date mydate,
      time mytime,
      timestamp mytimestamp
   ```
   자바의 Date 타입에는 년월일 시분초가 있지만 데이터베이스에는 date(날짜), time(시간), timestamp(날짜와 시간)라는 세 가지 타입이 별도로 존재합니다.   
   
   <span style="color:red">*Java 8 이후에는 java.time 패키지의 LocalDate, LodalTime, LocalDateTime을 사용할 경우 적용하지 않습니다.</span>    

1. # @AllArgsConstructor
   모든 필드를 포함하는 생성자를 자동으로 생성해 줍니다.    

   🔹 예제 코드    
   1️⃣ @AllArgsConstructor 없이 직접 생성자 작성    
   ```java
      public class Member {
         private String name;
         private int age;
         private String email;

         // 모든 필드를 포함하는 생성자
         public Member(String name, int age, String email) {
            this.name = name;
            this.age = age;
            this.email = email;
         }
      }

   ```

   2️⃣ @AllArgsConstructor 사용   
   ```java
      import lombok.AllArgsConstructor;

      @AllArgsConstructor  // 모든 필드를 매개변수로 받는 생성자 자동 생성
      public class Member {
         private String name;
         private int age;
         private String email;
      }
   ```   
   
   



