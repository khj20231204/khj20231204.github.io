---
layout: single
title: JPA - 페이징 API
categories: JPA
tab: []
---

1. # 페이징 API
   JPA는 페이징을 다음 두 API로 추상화 함   
   ```java     
      setFirstResult(int startPosition) // 조회 시작 위치(0부터 시작)

      setMaxResults(int maxResult) // 조회할 데이터 수
   ```   

1. # 페이징 API 예시
   ```java
      //페이징 쿼리
      String jpql = "select m from Member m order by m.name desc";
      List<Member> resultList = em.createQuery(jpql, Member.class)
      .setFristResult(10)
      .setMaxResults(20)
      .getResultList();
   ```  

1. # 예시
   ```java
      for(int i=2 ; i<50 ; i++){
         Member member2 = new Member();
         if(i<10){
            member2.setUsername("username 0" + i);
         }else{
            member2.setUsername("username " + i);
         }
         member2.setAge(i+10);
         em.persist(member2);
      }
      
      em.flush();
      em.clear();

      String pagingQuery = "select m from Member m order by m.username desc";
      List<Member> pagingList = em.createQuery(pagingQuery, Member.class)
                           .setFirstResult(1)
                           .setMaxResults(20)
                           .getResultList();

      for(Member m : pagingList){
            System.out.println(m.getUsername());
            System.out.println(m.getAge());
      }

      tx.commit();

      //결과 
      Hibernate: 
      /* select
         m 
      from
         Member m 
      order by
         m.username desc */ select
            m1_0.id,
            m1_0.city,
            m1_0.street,
            m1_0.zipcode,
            m1_0.age,
            m1_0.endDate,
            m1_0.startDate,
            m1_0.TEAM_ID,
            m1_0.username 
        from
            Member m1_0 
        order by
            m1_0.username desc 
        offset
            ? rows 
        fetch
            first ? rows only
      username 48
      58
      username 47
      57
      username 46
      56
      username 45
      55
      username 44
      54
      username 43
      53
      username 42
      52
      username 41
      51
      username 40
      50
      username 39
      49
      username 38
      48
      username 37
      47
      username 36
      46
      username 35
      45
      username 34
      44
      username 33
      43
      username 32
      42
      username 31
      41
      username 30
      40
      username 29
      39
   ```   