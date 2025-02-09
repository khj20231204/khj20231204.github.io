---
layout: single
title: JPA 연관 관계 
categories: JPA
tag: []
author_profile: false
---

1. # 연관 관계의 이해   
   JPA에서 연관관계는 영속객체(Entity)간의 관계를 의미합니다.   
   영속객체 간의 연관관계는 __방향성__ 을 가지며, 단방향, 양방향 그 특성에 따라 구분합니다.   
   연관관계는 관계의 __다중성__ 에 따라 일대일(1:1), 일대다(1:N), 다대일(N:1) 관계로 구분합니다.   
   영속객체가 테이블과 맵핑되는 것과 마찬가지로 영속객체간의 관계는 테이블간의 관계와 매핑됩니다.   
   영속객체간 관계 그리고 테이블간 관계에는 차이가 있으므로 이를 이해하고 매핑을 구성하는 것이 중요.   

1. # 연관 관계의 방향성(1/3) - @ManyToOne, @JoinColumn   
   영속객체 간의 관계는 방향성을 갖습니다. Student클래스가 Major클래스를 참조함으로 Student -> Major의 방향성을 갖습니다.   
   따라서, Student 객체는 참조하는 major를 통해 Major의 인스턴스 객체에 접근할 수 있습니다.   
   또한 하나의 Major를 다수의 Student가 참조하기 때문에 N:1의 관계를 갖습니다.   
   Student클래스는 Major클래스에 대해 ManyToOne의 관계, 그 반대의 경우에는 OneToMany의 관계가 됩니다.   

   ```java
      @Entity
      @Table(name="STUDENT_TB")
      public class Student{

         @Id
         @GeneratedValue
         private Long studentId;
         private String name;
         private String grade;

         @ManyToOne
         /*
         * Many는 Student
         * One는 Major
         * 현재클래스(Student) To 참조되는클래스(Major)
         *
         * Student 1명 - Major 1개
         * Major 1개 - Student 여러명
         *
         * 손님 1명 - 메뉴 여러개
         * 메뉴 1개 - 손님 1명
         * 주문 - 손님 여러명, 메뉴 여러개
         * 주문 테이블에 ManyToMany 관계
         * */
         @JoinColumn(name="MAJORID")
         private Major major;

         public Student(String name, String grade){
            this.name = name;
            this.grade = grade;
         }
      }
   ```   
   *ManyToMany   
   손님 1명 - 메뉴 여러개   
   메뉴 1개 - 손님 1명   
   주문 - 손님 여러명, 메뉴 여러개   
   주문 테이블에 ManyToMany 관계   

1. # JpaRepository
   ```java      
      @Repository
      public interface BoardRepository extends JpaRepository<Board, Integer>{

      //	public Board save(Board board);				// 글작성, 글수정 
      //	public long count();						// 글 갯수 
      //	public void delete(Board board);			// 글삭제 
      // public Board findByNo(int no);				// 상세 정보
         
         // JPQL
         @Query(value="select * from boards order by no desc limit :start, 10", nativeQuery = true)
         public List<Board> findAll(@Param("start")  int start);		// 전체 목록 검색	
      }
   ```   

   BoardRepository가 JpaRepository<Board, Integer>를 상속받았기 때문에   
   ```java
      //	public Board save(Board board);				// 글작성, 글수정 
      //	public long count();						// 글 갯수 
      //	public void delete(Board board);			// 글삭제 
      // public Board findByNo(int no);				// 상세 정보
   ```   
   다음을 주석처리해도 모든 기능을 수행할 수 있습니다.   

   JpaRepository<T, ID>는 CrudRepository<T, ID>와 PagingAndSortingRepository<T, ID>를 포함하며, 기본적인 CRUD 메서드를 제공합니다. JpaRepository를 상속받으면 아래와 같은 메서드들을 따로 정의하지 않아도 자동으로 사용할 수 있습니다.   

   __JpaRepository가 제공하는 주요 메서드__   
   + save(S entity): 엔티티 저장 및 수정   
   + findById(ID id): 특정 ID로 조회   
   + findAll(): 전체 조회   
   + count(): 레코드 개수 반환   
   + delete(T entity): 엔티티 삭제   
   + deleteById(ID id): ID로 엔티티 삭제   




   

   



