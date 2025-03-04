---
layout: single
title: JPA - 서브쿼리
categories: JPA
tab: []
---

1. # 서브 쿼리
   
   __나이가 평균보다 많은 회원__   
   ```sql
      select m from Member m
      where m.age > (select avg(m2.age) from Member m2)
   ```   
   외부 Member의 m을 서브쿼리고 가져오지 않고 서브쿼리에서는 Member m2로 새로 정의했다. 이렇게 해야 성능이 잘 나온다.   

   __한 건이라도 주문한 고객__   
   ```sql
      select m from Member m
      where (select count(o) from Order o where m = o.member) > 0
   ```   
   외부 Member의 m을 서브쿼리고 가져와서 m = o.member 이렇게 Order의 member와 비교하고 있다. 이러면 위에 경우보다 성능이 안 좋다. 이렇게 일반적인 서브쿼리도 지원한다.   

1. # 서브 쿼리 지원 함수
   1.[NOT] EXISTS (subquery 문) : 서브쿼리에 결과가 존재하면 참   
      · {ALL | ANY | SOME} (subquery 문)   
      · ALL 모두 만족하면 참   
      · ANY, SOME : 같은 의미, 조건을 하나라도 만족하면 참   
   2.[NOT] IN (subquery 문) : 서브쿼리의 결과 중 하나라도 같은 것이 있으면 참   

1. # 서브 쿼리 - 예제
   · 팀 A 소속인 회원   
   ```sql
      select m from Member m
      where exists (select t from m.team t where t.name = '팀A')
   ```   

   · 전체 상품 각각의 재고보다 주문량이 많은 주문들   
   ```sql
      select o from Order o
      where o.orderAmount > ALL (select p.stockAmout from Product p)
   ```   

   · 어떤 팀이든 팀에 소속된 회원   
   ```sql
      select m from Member m
      where m.team = ANY (select t from Team t)
   ```   

1. # 하이버네이트6 변경 사항
   하이버네이트6 부터는 FROM 서브쿼리를 지원합니다.   

   · https://in.relation.to/2022/06/24/hibernate-orm-61-
features/

1. # JPA 서브 쿼리 한계
   · JPA는 WHERE, HAVING 절에서만 서브 쿼리 사용 가능   
   · SELECT 절도 가능(하이버네이트에서 지원)   
   · FROM 절의 서브 쿼리는 현재 JPQL에서 불가능   
   -> 조인으로 풀 수 있으면 풀어서 해결   