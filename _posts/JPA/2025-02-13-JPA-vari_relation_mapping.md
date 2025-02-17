---
layout: single
title: JPA - 다양한 연관관계 매핑
categories: JPA
tab: []
---

1. # 연관관계 매핑시 고려사항 
   1.다중성   
   2.단방향, 양방향   
   3.연관관계의 주인   

1. # 다중성
   1.다대일 : @ManyToOne   

   2.일대다 : @OneToMany   

   3.일대일 : @OneToOne   

   4.다대다 : @ManyToMany   

1. # 단방향, 양방향
   테이블   
   1.외래 키 하나로 양쪽 조인 가능   
   2.방향이라는 개념이 없음   

   객체   
   1.참조용 필드가 있는 쪽으로만 참조 가능   
   2.한쪽만 참조하면 단방향   
   3.양쪽이 서로 참조하면 양방향   

1. # 다대일 단방향

   <img src="../../imgs/jpa/manytoone.png" style="border:3px solid black;border-radius:9px;width:600px">    

   ```java
      //Member클래스
      public class Member{

         @Id @GeneratedValue
         @Column(name = "MEMBER_ID")
         private Long id;

         ...

         @ManyToOne //Member이 다 : Team이 1 이된다
         @joinColumn(name = "TEAM_ID") //Team클래스의 컬럼명 => TEAM_ID, 조인 컬럼 설정
         private Team team;

         ...
      }

      //Team클래스
      public class Team{

         ...

         @Id @GeneratedValue
         @Column(name = "TEAM_ID")
         private Long id;

         ...
      }
   ```   
   Many부분에 Team의 FK를 포함

1. # 다대일 양방향   
   <img src="../../imgs/jpa/manytoone2.png" style="border:3px solid black;border-radius:9px;width:600px">     

   ```java
      //Member클래스
      public class Member{

         @Id @GeneratedValue
         @Column(name = "MEMBER_ID")
         private Long id;

         ...

         @ManyToOne //Member이 다 : Team이 1 이된다
         @joinColumn(name = "TEAM_ID") //Team클래스의 컬럼명 => TEAM_ID, 조인 컬럼 설정 
         private Team team;  

         ...
      }

      //Team클래스
      public class Team{

         ...

         @Id @GeneratedValue
         @Column(name = "TEAM_ID")
         private Long id;

         ...

         @OneToMany(mappedBy = "team")  //mappedBy의 값이 주인이 되며 필드명이다
         private List<Member> members = new ArrayList<>(); //양방향을 위해 추가. members.team이 맵핑
      }
   ```   
   단방향에서 양방향을 추가 한다고해서 테이블에 영향을 주지 않는다. 그렇기 때문에 단방향 설계를 모두한 이후에 필요에 따라 양방향으로 설정하면 된다.   
   Many부분이 FK를 포함하고 연관관계의 주인이 된다.   
   
   @OneToMany(mappedBy = "team")   
   private List<Member> members = new ArrayList<>()   
   의미 : Member엔티티의 team필드가 주인이며, 외래키 값을 관리하는 것은 Member엔티티의 team필드이다   

   이 소스 부분을 통해 Team에서도 member를 조회할 수 있다(조회만 가능)   

1. # 일대일 단방향 

   Member와 Locker가 있을 때 한명의 멤버가 하나의 락커만 사용가능 하다고 가정   

   Member클래스에서 Locker클래스를 참조   
   ```java
      //Member클래스
      @Entity
      class Member{
         ...

         @OneToOne
         @JoinColumn(name = "LOCKER_ID")
         private Locker locker;

         ...
      }

      //Locker클래스
      @Entity
      public class Locker {
         ...

         @Id @GeneratedValue
         @Column(name = "LOCKER_ID")
         private Long id;
         ...
      }
   ```

   Locker클래스에서 Member클래스를 참조   
   ```java
      //Member클래스
      @Entity
      class Member{
         
         @Id @GeneratedValue
         @Column(name = "MEMBER_ID")
         private Long id;
         
         ...
      }

      //Locker클래스
      @Entity
      public class Locker {
         ...
         
         @OneToOne
         @joinColumn(name = "Member_id")
         private Member member;
         ...
      }
   ```

1. # 일대일 양방향 

   ManyToOne 방식과 같이 단방향 방식에서 양방향 List가 필요한 컬럼에 추가하면 됩니다.   

   Member클래스에서 Locker클래스를 참조한 구조에서의 양방향   
   ```java
      //Member클래스
      @Entity
      class Member{
         ...

         @OneToOne
         @JoinColumn(name = "LOCKER_ID")
         private Locker locker;

         ...
      }

      //Locker클래스
      @Entity
      public class Locker {
         ...

         @Id @GeneratedValue
         @Column(name = "LOCKER_ID")
         private Long id;
         ...

         @OneToOne(mappedBy = "locker")
         private List<Member> members = new ArrayList<>(); //이걸 추가해주므로 Locker에서도 member에 접근 가능
      }
   ```

   *일대다와 다대다는 잘 사용하지 않으므로 생략
   

