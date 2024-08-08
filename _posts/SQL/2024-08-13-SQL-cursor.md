---
layout: single
title: cursor(커서)
categories: SQL
tag: [cross, 레코드 수 문제]
---

1. #  커서
   행 단위 처리를 하기 위해서 사용하는 메커니즘 입니다. 2개 이상의 데이터를 처리할 때 커서를 사용합니다.   

   ```sql
      DECLARE
         
         --커서 선언
         CURSOR cursor_name IS statement,       -- 1)

      BEGIN

         --커서 열기
         OPEN cursor_name;                      -- 2)

         --커서로부터 데이터를 읽어와 변수에 저장
         FETCH  cursor_name INTO variable_name; -- 3)

         --커서 닫기
         CLOSE cursor_name;                     -- 4)

      END;
   ```   

   <img src="../../imgs/sql/cursor_flow.png" style="boder:3px solid black;boder-radius:9px;width:500px">   

   1)
   ```
      CURSOR cursor_name IS statement;
   ```   
   cursor_name : PL/SQL 식별자   
   statement : INTO절이 없는 SELECT문장   

   2)
   ```
      OPEN cursor_name;   
   ```
   질의를 수행하고 검색 조건을 충족하는 모든 행으로 구성된 결과 셋을 생성하기 위해 CURSOR를 OPEN합니다. CURSOR는 이제 결과 셋에서 첫 번째 행을 가리킵니다.   
   ex)OPEN C1;   
   C1을 오픈하면 검색 조건에 만족하는 모든 행으로 구성된 결과 셋이 구해지고 __부서 테이블의 첫 번째 행을 가리키게 됩니다.__   
   
   3)
   ```
      FETCH cursor_name into {variable1[,variable2, ....]};
   ```
   FETCH 문은 결과 셋에서 로우 단위로 데이터를 읽어 들입니다. 각 인출(FETCH) 후에 CURSOR는 결과 셋에서 다음 행으로 이동합니다. FETCH 문장은 현재 행에 대한 정보를 얻어 와서 INTO 뒤에 기술한 변수에 저장한 후 다음 행으로 이동합니다. 얻어진 여러 개의 로우에 대한 결과값을 모두 처리하려면    


   
   