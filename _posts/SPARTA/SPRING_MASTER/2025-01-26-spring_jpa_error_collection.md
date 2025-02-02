---
layout: single
title: JPA 에러 모음
categories: SPRING_MASTER
tag: []
author_profile: false
---
 
1. # 2개 테이블 생성시 insert가 안되는 이유
   ```   
      major클래스는 다음과 같다
      package com.jpa.entity;

      import jakarta.persistence.*;
      import lombok.Data;
      import lombok.NoArgsConstructor;

      import java.util.List;

      @Data
      @Entity
      @Table(name="MAJOR_TB")
      @NoArgsConstructor
      public class Major {

         @Id
         @GeneratedValue
         private Long majorId;

         private String name;

         private String category;

         public Major(String name, String category) {
            this.name = name;
            this.category = category;
         }
      }

      Student 클래스는 다음과 같다
      package com.jpa.entity;


      import jakarta.persistence.Entity;
      import jakarta.persistence.GeneratedValue;
      import jakarta.persistence.Id;
      import jakarta.persistence.Table;
      import lombok.Data;
      import lombok.NoArgsConstructor;

      @Data
      @NoArgsConstructor
      @Entity
      @Table(name="STUDENT_TB")
      public class Student {

         @Id
         @GeneratedValue
         private Long studentId;

         private String name;

         private String grade;

         private Long majorId;

         public Student(String name, String grade) {
            this.name = name;
            this.grade = grade;
         }
      }

      실제 MAIN으로 실행한 코드이다
      {
      Major major = new Major("Computer Science","Engineer");
                  em.persist(major);

                  Student student = new Student("Jack","3");
                  student.setMajorId(major.getMajorId());
                  em.persist(student);

                  tx.commit();
      }
      이때 다음과 같은 코드가 있을 때 왜 MAJOR_TB와 STUDENT_TB 테이블에 왜 데이터가 삽입안되는가
   ```   

   답변:     
      데이터가 MAJOR_TB와 STUDENT_TB 테이블에 삽입되지 않는 이유는 Major 엔티티를 persist()한 후, Major의 majorId가 Student 객체에 반영되지 않았기 때문입니다.   
      
      1.majorId가 null인 상태에서 student의 majorId를 설정함   
         majorId는 @GeneratedValue로 자동 생성됩니다.   
         하지만 em.persist(major);를 실행한 직후에는 영속성 컨텍스트에 저장만 되고, 즉시 majorId가 데이터베이스에서 반영되지 않습니다.   
         따라서 major.getMajorId()를 호출하면 아직 null을 반환할 가능성이 큽니다.   
         이후 student.setMajorId(major.getMajorId());를 호출하면 null이 설정되므로, STUDENT_TB의 majorId가 null로 들어가게 됩니다.   

      2.JPA에서 persist() 후에도 즉시 majorId가 반영되지 않음   
         persist()를 호출해도 즉시 데이터베이스에 반영되지 않고, 트랜잭션이 커밋되거나 플러시될 때 반영됩니다.   
         major.getMajorId()를 호출할 시점에는 아직 majorId가 할당되지 않았을 가능성이 있습니다.   

      🛠 해결 방법   
      ✅ 해결 방법 1: flush()를 사용하여 majorId를 즉시 반영   
      ```java
         Major major = new Major("Computer Science", "Engineer");
         em.persist(major);
         em.flush(); // 여기서 flush를 호출하여 majorId가 즉시 반영되도록 함

         Student student = new Student("Jack", "3");
         student.setMajorId(major.getMajorId());
         em.persist(student);

         tx.commit();
      ```
      💡 flush()를 호출하면 JPA는 현재 영속성 컨텍스트에 있는 변경 내용을 즉시 DB에 반영하고, majorId 값도 채워집니다.   

      ✅ 해결 방법 2: majorId 대신 Major 객체 자체를 Student에 저장   
      현재 Student 클래스에서 majorId를 Long 타입으로 관리하는 대신, JPA 연관 관계를 설정하면 더욱 깔끔하게 해결할 수 있습니다.   

      🔹 Major ↔ Student 관계 설정 (One-to-Many, Many-to-One)   
      ```java
         @Entity
         @Table(name="STUDENT_TB")
         public class Student {

            @Id
            @GeneratedValue
            private Long studentId;

            private String name;
            private String grade;

            @ManyToOne
            @JoinColumn(name = "major_id") // STUDENT_TB 테이블의 외래키 컬럼명
            private Major major;

            public Student(String name, String grade, Major major) {
               this.name = name;
               this.grade = grade;
               this.major = major;
            }
         }
      ```
      @ManyToOne을 사용하면 student.setMajorId(major.getMajorId()); 대신 student.setMajor(major);로 설정할 수 있습니다.   
      Major 엔티티와 Student 엔티티 간의 관계가 자연스럽게 유지됩니다.   
      🔹 코드 수정   
      ```java
         Major major = new Major("Computer Science", "Engineer");
         em.persist(major);

         Student student = new Student("Jack", "3", major);
         em.persist(student);

         tx.commit();
      ```   
      💡 JPA 연관 관계를 올바르게 설정하면 flush() 없이도 majorId가 올바르게 저장됩니다.   

1. # insert되지 않고 Exception이 발생하는 이유

   ```java
      @NoArgsConstructor
      @Entity
      @Table(name="customer_tb")
      @Data
      @TableGenerator(name="id_generator", table="customer_id",pkColumnName = "id_name", pkColumnValue = "customer_id", initialValue = 1, allocationSize = 1)
      public class Customer {

         @Id
         @GeneratedValue(strategy = GenerationType.IDENTITY)
         private String id;
         private String name;
         private Long registerDate;

         public Customer(String id, String name) {
            this.id = id;
            this.name = name;
            this.registerDate = System.currentTimeMillis();
         }

         public static Customer sample(){
            return new Customer("1000","test2");
         }
      }

      다음 코드는 main에서 실행하는 코드이다
      public class CustomerJpaExam {
         public static void main(String[] args) {
            CustomerJpaExamGeneratedValue cjgv = new CustomerJpaExamGeneratedValue();

            EntityManagerFactory emf = Persistence.createEntityManagerFactory("customer-exam");
            EntityManager em = emf.createEntityManager();
            EntityTransaction tx = em.getTransaction();

            tx.begin();
            try{
                  em.persist(Customer.sample()); //입력 insert
            }catch(Exception e){
                  System.out.println(e);
                  tx.rollback();
            }finally{
                  em.close();
            }
            emf.close();
         }
      }

      왜 exception 에러가 발생하는가
   ```
   코드에서 예외가 발생하는 주요 원인은 @GeneratedValue(strategy = GenerationType.IDENTITY)가 적용된 id 필드가 String 타입이기 때문입니다.   
   
   코드 수정   
   ```java
      @Entity
      @Table(name="customer_tb")
      @Data
      @NoArgsConstructor
      public class Customer {

         @Id
         @GeneratedValue(strategy = GenerationType.IDENTITY)
         private Long id; // 🔹 id를 Long 타입으로 변경

         private String name;
         private Long registerDate;

         public Customer(String name) {  // 🔹 id는 자동 생성되므로 생성자에서 제거
            this.name = name;
            this.registerDate = System.currentTimeMillis();
         }

         public static Customer sample(){
            return new Customer("test2");  // 🔹 id를 제거하고 이름만 넘김
         }
      }
   ```

1. # entity로 생성될 객체 이름이 persistence.xml에 존재해야됨

   ```java
      //main 부분
      EntityManagerFactory emf = Persistence.createEntityManagerFactory("customer-exam");
      EntityManager em = emf.createEntityManager();
      EntityTransaction tx = em.getTransaction();

      //EntityManagerFactory의 customer-exam이 persistence.xml파일에 존재 해야됨

      //persistence.xml 파일 부분
      <persistence-unit name="customer-exam">
        <properties>
        ...
   ```
   main부분의 customer-exam가 persistence.xml의 persistence-unit에 존재해야 됨

1. # 