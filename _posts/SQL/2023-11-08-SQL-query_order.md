---
layout: single
title: 쿼리 순서
categories: SQL
tag: [쿼리 순서]
---

1. # 일반 쿼리 순서
   SELECT ...     
   FROM ...   
   WHERE ...   
   GROUP BY ...   
   HAVING ...   
   ORDER BY ...

   FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY

1. # JOIN에서 쿼리 순서
   SELECT ...
   FROM ... JOIN ...
   ON ... 
   WHERE ...
   GROUP BY ...
   HAVING ...
   ORDER BY ...

   2. FROM 절: 먼저 FROM 절에 지정된 테이블들이 조인되어 가상의 결과 집합이 생성됩니다. 이때, 테이블 간의 조인은 FROM 절에 지정된 순서대로 이루어집니다.

   2. ON 절: ON 절은 JOIN 절에서 조인할 때 사용되며, JOIN 조건을 지정합니다. ON 절은 FROM 절의 결과 집합에 대해 조인을 수행하기 전에 실행됩니다. ON 절에서는 테이블 간의 조인 조건을 지정하여 어떤 열이 서로 매칭되는지를 결정합니다.
   
   2. JOIN 절: JOIN 절은 FROM 절에서 생성된 결과 집합에 추가적인 테이블을 조인하는 역할을 합니다. JOIN 절에서는 추가적인 테이블과 기존 결과 집합 간의 조인 방식을 지정합니다. 여러 개의 JOIN 절이 존재할 경우, 순서대로 조인이 수행됩니다.

   따라서, ON 절은 JOIN 절에서 사용되는 조인 조건을 먼저 실행하고, 그 후에 JOIN 절에서 테이블 간의 조인이 수행됩니다. 이렇게 함으로써 테이블들이 조인되고, 조인된 결과를 이용하여 다음 단계인 WHERE 절 등에서 조건을 평가하게 됩니다.

   2. WHERE 절: WHERE 절은 FROM 절과 JOIN 절에서 생성된 결과 집합에 대해 조건을 지정합니다. WHERE 절은 조인된 결과 집합에서 특정 조건을 만족하는 행들을 추출하는 역할을 합니다. WHERE 절은 모든 조인이 완료된 후에 실행됩니다.

   따라서, FROM 절과 JOIN 절은 테이블 간의 조인을 수행하고, ON 절은 조인 조건을 지정합니다. 그리고 WHERE 절은 조인된 결과 집합에서 특정 조건을 만족하는 행들을 추출하는 역할을 합니다. 이러한 순서로 SQL 문이 실행되며, 결과 집합이 생성됩니다.

   2. GROUP BY → HAVING → SELECT → ORDER BY

1. # 메인 쿼리란?
   SQL에서 메인 쿼리의 범위는 일반적으로 SELECT 문을 포함하는 전체 쿼리를 의미합니다. 즉, 메인 쿼리는 SELECT 문과 함께 FROM, WHERE, GROUP BY, HAVING, ORDER BY 등의 다른 절들을 포함하는 전체 쿼리를 말합니다. 이 범위 내에서 메인 쿼리를 실행하고 결과를 반환합니다. 반대로, 연관 서브쿼리는 메인 쿼리 내에 포함되어 메인 쿼리의 실행 중에 각 행마다 실행되는 서브쿼리를 의미합니다.

1. # 메인쿼리와 서브쿼리 순서

   2. 메인쿼리의 실행: 먼저 메인쿼리가 실행되며, 결과 집합을 생성합니다.

   2. 서브쿼리의 실행: 메인쿼리의 실행 도중 서브쿼리가 포함되어 있다면, 서브쿼리가 실행됩니다. 서브쿼리의 결과는 메인쿼리의 실행에 영향을 줄 수 있습니다.

   2. 서브쿼리의 결과를 메인쿼리에 적용: 서브쿼리의 실행이 완료되면, 그 결과를 메인쿼리에 적용하여 최종 결과 집합을 생성합니다. 이때 서브쿼리의 결과를 사용하여 조건식을 평가하거나, 서브쿼리의 결과를 테이블로 간주하여 조인을 수행할 수 있습니다.

   즉, 서브쿼리는 메인쿼리의 실행 도중에 실행되며, 그 결과는 메인쿼리의 실행에 영향을 줄 수 있습니다. 따라서 서브쿼리의 결과를 이용하여 원하는 결과를 얻기 위해서는 서브쿼리의 실행 순서와 결과를 잘 이해하고 활용해야 합니다.

1. # 메인쿼리와 연관서브쿼리 순서
   - 연관 서브쿼리 동작 방식   
   연관 서브쿼리는 __메인 쿼리의 각 행에 대해 실행__ 되는 쿼리입니다. 즉, 메인 쿼리가 여러 개의 행을 반환할 때, 연관 서브쿼리는 메인 쿼리의 각 행을 하나씩 가져와서 실행합니다. 연관 서브쿼리는 메인 쿼리의 각 행에 대해 별도의 실행을 수행하며, 메인 쿼리의 결과에 따라 동적으로 실행되기 때문에 결과도 각 행마다 다를 수 있습니다. 이를 통해 연관 서브쿼리는 메인 쿼리의 데이터를 활용하여 조인, 필터링 또는 계산을 수행할 수 있습니다   

   - 예제)
   STUDENT테이블과 DEPARTMENT테이블입니다.   
   ```sql
      SELECT * FROM STUDENT;

      ST_NUM     ST_NAME    D_NUM
      ---------  ---------- ---------
      1001       yoo        10
      1002       kim        30
      1003       lee        20
      1004       park       10
      1005       choi       20
      1006       jeong      10


      SELECT * FROM DEPARTMENT;

      DEPT_NUM DEPT_NAME           
      -------- ---------------
      10       컴퓨터공학          
      20       원자력공학          
      30       전자계산학과   
   ```   

   연관서브쿼리 입니다.   
   ```sql
      SELECT ST_NAME, D_NUM
      FROM STUDENT S
      WHERE NOT EXISTS
      (SELECT *
      FROM DEPARTMENT D
      WHERE S.D_NUM = D.DEPT_NUM
      AND DEPT_NAME=’전자계산학과’
      )

      ST_NAME    D_NUM
      ---------- ----------
      choi       20
      lee        20
      jeong      10
      park       10
      yoo        10
   ```   
   메인 쿼리에서 STUDENT 테이블이 __한 행씩 읽힐 때마다__ S.D_NUM이 호출됩니다. 메인 쿼리의 SELECT 문에서 S.D_NUM은 STUDENT 테이블의 D_NUM 열을 나타내며, WHERE 절에서 조건을 확인하기 위해 한 행씩 읽어들이게 됩니다.   

   NOT EXISTS 절은 연관 서브쿼리의 결과가 없는 경우에만 참이 되므로, 메인 쿼리에서는 DEPARTMENT 테이블에서 DEPT_NAME이 ‘전자계산학과’인 학과에 속하지 않는 학생들만 선택됩니다. 서브쿼리에서 S.D_NUM이 한 행씩 호출되어 실행될 때마다 조건이 '전자계산학과'로 D_NUM이 30인 경우만 일치하여 NOT EXISTS가 FALSE가 되기 때문에 메인쿼리가 실행되지 않고 나머지 D_NUM이 10인 경우와 20인 경우에는 모두 실행이 됩니다.   

1. # 일반 서브쿼리와 연관 서브쿼리의 차이
   연관 서브쿼리는 메인 쿼리의 컬럼과 연관된 서브쿼리입니다. 이는 메인 쿼리의 각 행에 대해 별도로 실행되며, 메인 쿼리의 컬럼 값을 참조하여 결과를 반환합니다. 연관 서브쿼리는 메인 쿼리와 함께 실행되므로, 메인 쿼리의 실행이 완료되기 전에 연관 서브쿼리가 실행되는 것이 특징입니다.   
      
   반면, 일반 서브쿼리는 메인 쿼리와 독립적으로 실행되는 서브쿼리입니다. 메인 쿼리와는 독립적으로 실행되기 때문에 일반적으로 서브쿼리가 먼저 실행되고 그 결과를 메인 쿼리에 전달합니다.   
      
   따라서 연관 서브쿼리와 일반 서브쿼리는 실행 시점과 메인 쿼리와의 관계에서 차이가 있습니다.   
