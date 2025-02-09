---
layout: single
title: JPA - setting
categories: JPA
tab: []
---

1. # Setting
   persistence.xml

1. # 구동 방식
   1.설정 정보 조회  META-INF/persistence.xml   
   2.EntityManagerFactory 생성   
   3.EntityManager 생성   

   persistence.xml파일에서 환경을 읽어들여 설정을 하고 EntityMangerFactory에서 EntityManger를 생성합니다.   
   
1. # 주의
   1.엔티티 매니저 팩토리는 DB당 1개만 생성해서 애플리케이션 전체에서 공유   
   2.엔티티 매니저는 쓰레드간에 공유를 하면 안 된다(사용하고 버려야한다)   
   3.JPA의 모든 데이터 변경은(단수 select 제외) 트랜잭션 안에서 실행   

1. # update문에 persist를 사용하지 않아도 되는 이유
   JPA의 영속성에 의해서 모든 entity는 관리를 받고 있다. commit을 할 때 이전 데이터와 비교를 해서 다른 점이 있다면 update쿼리를 실행하고 commit을 한다

1. 