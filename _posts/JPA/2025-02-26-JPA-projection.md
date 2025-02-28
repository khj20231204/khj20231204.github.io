---
layout: single
title: JPA - 프로젝션
categories: JPA
tab: []
---

1. #  프로젝션
   1.SELECT 절에 조회할 대상을 지정하는 것   
   2.프로젝션 대상 : 엔티티, 임베디드 타입, 스칼라 타입(숫자, 문자등 기본 데이터 타입)   

   앞으로의 예제가 되는 Member.java클래스   
   ```java
      @Entity
      public class Member {
         
         @Id @GeneratedValue
         private Long id;
         private String username;
         private int age;

         @ManyToOne 
         @JoinColumn(name="TEAM_ID")
         private Team team;  //Team은 조인이 걸려 있는 엔티티

         @Embedded
         private Period period;

         @Embedded 
         private Address address;  //Address는 임베디드 타입
   ```

1. # 엔티티 프로젝션

      1)Member엔티티를 가져온다.   
      ```sql
         SELECT m FROM Member m -- 엔티티 프로젝션, m은 Member의 별칭   
      ```   

      예제)   
      ```java
         List<Member> result = em.createQuery("select m from Member m", Member.class).getResultList();
         //위에 쿼리 select m from Member m 로 가져온 m의 결과는 모두 영속성 컨텍스트에 저장이 되어 관리가 된다.   

         Member findMember = result.get(0);
         //List의 0번째 인텍스 값을 가져와서 
         
         findMember.setAge(30);
         //다시 변경하면 영속성 컨텍스트에 의해 관리가 되므로 변경이 가능
      ```

      2)Member와 Join되어 있는 Team엔티티를 가져온다
      ```sql   
         SELECT m.team FROM Member m -- 엔티티 프로젝션  
      ```   

      예제)   
      ```java
         List<Team> result2 = em.createQuery("select m.team from Member m", Team.class).getResultList();
         for(Team t : result2){
            System.out.println(t);
         }
      ```   
      m.team의 결과로 Team을 가져오기 때문에 `List<Team>` List의 제네릭타입으로 Team이 들어간다. Member와 Team을 Join을 해서 값을 가져오게 되는데 쿼리문에도 가독성을 위해 join이 보여야 하기 때문에 다음과 같이 하는 것이 맞다.   
      ```java
         List<Team> result2 = em.createQuery("select t from Member m join m.team t", Team.class).getResultList();
         for(Team t : result2){
               System.out.println(t);
         }
      ```   
      `select t from Member m join m.team t` 쿼리문에 join이 들어가게 작성을 해야한다.   


1. # 임베디드 타입 프로젝션
      ```sql
         SELECT m.address FROM Member m -- 임베디드 타입 프로젝션   
      ```   

      예제)   
      ```java
            List<Address> result3 = em.createQuery("select m.address from Member m", Address.class).getResultList();
            //또는
            List<Address> result3 = em.createQuery("select o.address from Order o", Address.class).getResultList();
            for(Address a : result3){
                System.out.println(a);
            }
      ```   
      `List<Address>`와  `Address.class` 처럼 가져오는 엔티티로 받는다.   
      m.address 와 o.address에서처럼 속해있는 엔티티를 명시해 줘야한다.      

1. # 스칼라 타입 프로젝션
      ```sql
         SELECT m.username, m.age FROM Member m -- 스칼라 타입 프로젝션   
      ```   

      ```java
         List<MemberDTO> result = em.createQuery("select myjpql.MemberDTO(m.username, m.age) from Member m").getResultList();
      ```   

      스칼라 타입이란?   
      *스칼라 타입(Scalar Type)은 엔티티가 아닌 단순한 값(필드 값, 기본 데이터 타입 등)을 의미합니다. 즉, JPQL에서 특정 컬럼(필드)만 선택하여 가져오는 경우, 해당 값들은 스칼라 타입 입니다.   
      
      *distinct로 중복 제거 

1. # 프로젝션 - 여러 값 조회
   1.Query 타입으로 조회   
   ```java
      List result4 = em.createQuery("select m.username , m.age from Member m").getResultList();

      Object obj = result4.get(0);
      Object[] obj2 = (Object[])obj;
      System.out.println("obj2[0]-username : " + obj2[0]);
      System.out.println("obj2[1]-age : " + obj2[1]);
   ```   

   2.Object[] 타입으로 조회   
   ```java
      List<Object[]> result5 = em.createQuery("select m.username, m.age from Member m").getResultList();

      for(Object[] o : result5){
            String username = (String)o[0];
            int age = (int)o[1];
            System.out.println("username:"+username+" ,age:"+age);
      }
   ```    
   
   3.new 명령어로 조회 -  JPQL에서 권장하는 조회 방법   
   ```java
      List<MemberDTO> result6 = em.createQuery("select new myjpql.MemberDTO(m.username, m.age) from Member m", MemberDTO.class).getResultList();
      for(MemberDTO md : result6){
            System.out.println("username:"+md.getUsername()+" ,age:"+md.getAge());
      }
   ```   
   
   3-1)MemberDTO를 생성한다.   
   순서와 타입이 일치하는 생성자가 필요. 쿼리문에서 username과 age를 가져오기 때문에 해당 필드를 포함하는 생성자를 만들고 Getter과 Setter도 만든다.   
   ```java
      public class MemberDTO {

         private String username;
         private int age;
         
         //쿼리문에서 넣을 변수를 포함하는 생성자를 만들어야 한다
         public MemberDTO(String username, int age) {
            this.username = username;
            this.age = age;
         }
         public String getUsername() {
            return username;
         }
         public void setUsername(String username) {
            this.username = username;
         }
         public int getAge() {
            return age;
         }
         public void setAge(int age) {
            this.age = age;
         }
      }
   ```   
   3-2)패키지 명을 포함한 전체 클래스 명 입력   
   쿼리문은 문자이기 때문에 패키지명을 문자로 다 입력해줘야 한다   
   `new myjpql.MemberDTO(m.username, m.age)`
   
   3-3)new 연산자 사용   
   조회한 데이터를 특정 DTO 객체로 직접 변환하기 위해서 new 연산자를 사용합니다. new 연산자를 사용하므로써 JPQL 결과를 직접 DTO에 매핑할 수 있다.   

1. # Address.class의 유무
   1.Address.class가 있는 경우   
   ```java
      List<Address> result3 = em.createQuery("select o.address from Order o", Address.class).getResultList();
   ```   
   🔹 이유: 단일 타입 프로젝션   
   select o.address → 단일 필드(Address)만 선택   
   Address.class 를 지정 → JPQL이 Address 타입을 예상할 수 있음
   반환 타입이 List<Address> 가 됨   
   👉 쿼리 결과가 Address 객체 리스트이므로, Address.class를 지정할 수 있음   

   2.Address.class가 없는 경우   
   ```java
      List result4 = em.createQuery("select m.username , m.age from Member m").getResultList();
   ```   
   🔹 이유: 다중 필드(스칼라 값) 프로젝션   
   select m.username, m.age → 여러 필드(username, age)를 선택
   단일 엔티티나 임베디드 타입이 아닌 다중 값(스칼라 타입) 조회
   List<Object[]> 형태로 결과가 반환됨 (즉, 개별 요소가 Object[] 배열)   
   createQuery에서 특정 클래스(Address.class 등)를 지정할 수 없음   
   👉 JPQL이 여러 개의 값을 반환할 때는 특정 엔티티 타입을 지정할 수 없음   
   👉 결과는 List<Object[]> 형태로 받게 됨   

