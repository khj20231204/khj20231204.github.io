---
layout: single
title: JPA - 연관관계 매핑
categories: JPA
tab: []
---

1. # 객체와 테이블 연관관계의 차이를 이해

1. # 객체의 참조와 테이블의 외래 키를 매핑

1. # 용어 이해
   방향(Direction) : 단방향, 양방향   
   다중성(Multiplicity) : 다대일(N:1), 일대다(1:N), 일대일(1:1), 다대다(N:N)   
   연관관계의 주인(Owner) : 객체 양방향 연관관계는 관리   

1. # 단방향 연관관계 예제 시나리오
   회원과 팀이 있다.   
   회원은 하나의 팀에만 소속될 수 있다.   
   회원과 팀은 다대일 관계이다.   

   ```java
      //Team객체
      @Entity
      public class Team {
         
         @Id @GeneratedValue
         private Long id;
         private String name;
      }

      //Member객체
      @Entity
      class MemberOfTeam{

         @Id @GeneratedValue
         private Long id;

         @Column(name = "USER_NAME")
         private String name;
         private int age;

         //@Column(name = "TEAM_ID")
         //private Long teamId;

         @ManyToOne //MemberOfTeam입장 To Team입장
         @JoinColumn(name = "TEAM_ID")  //Join하는 컬럼이 TEAM_ID이다. 이 TEAM_ID는 DB에 존재하는 컬럼.
         private Team team;
      }
   ```   
   팀은 1개, 멤버는 여러명 => 멤버가 팀을 포함, 멤버에서 팀을 참조   
   <img src="../../imgs/jpa/member_team.png" style="border:3px solid black;border-radius:9px;width:600px">     

   ```java
      public static void main(String[] args) {
        //basic_execute();
        //columnMapping();

        EntityManagerFactory emf = Persistence.createEntityManagerFactory("hello");
        EntityManager em = emf.createEntityManager();
        EntityTransaction tx = em.getTransaction();

        tx.begin();

        try{

            Team team = new Team();
            team.setName("TeamA");
            em.persist(team);
           
            MemberOfTeam member = new MemberOfTeam();

            member.setName("member1");
            
            //mot.setTeamId(team.getId()); //위에 persist를 하면 영속상태가 되고 자동으로 team에 id값이 입력된다. 
            
            //이제 getId로 team의 pk를 넣는게 아니라 team클래스 자체를 넣는다
            member.setTeam(team);  
            
            em.persist(member);

            /* 
            persist를 하면 영속성 컨텍스트의 캐쉬에 값이 저장된다 밑에 find로 찾은 값은 영속성 컨텍스트의 캐쉬에 있는 값이다.
            영속성 컨텍스트 말고 DB에서 바로 값을 불러오고 싶으면 다음과 같이 하면 된다
            */
            em.flush(); //sql문을 날려서 DB에 강제 저장
            em.clear(); //영속성 컨텍스 값을 초기화. 이렇게하면 영속성 컨텍스트의 캐쉬에 값이 없기 때문에 DB에서 찾아서 바로 가져온다

            MemberOfTeam findmember = em.find(MemberOfTeam.class, member.getId());
            
            //Team findteam = em.find(Team.class, findmember.getTeamId());
            //이제 findmember인 찾은 멤버에서 바로 team을 불러온다
            Team findteam = findmember.getTeam();

            System.out.println("------------------------------------"+findteam.getName());

            /*
            수정 - DB에 10번 팀이 있다고 가정하고 팀을 10번 팀으로 바꾸는 경우
            Team newTeam = em.find(Team.class, 10L);
            findmember.setTeam(newTeam); //setTeam으로 그냥 team을 입력하면 끝
            */
            tx.commit();

        } catch (Exception e) {
            tx.rollback();
            throw new RuntimeException(e);
        }finally {
            em.close();
        }
        emf.close();
    }
   ```

1. # 양방향 연관관계
    