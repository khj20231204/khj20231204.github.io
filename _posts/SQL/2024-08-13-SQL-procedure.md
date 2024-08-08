---
layout: single
title: 프로시져
categories: SQL
tag: [cross, 레코드 수 문제]
---


1. # Procedure(프로시저)
   저장 프로시져를 생성하려면 CREATE PROCEDURE다음에 새롭게 생성하고자하는 프로지셔 이름을 기술합니다. 이렇게 해서 생성한 저장 프로시저는 여러 번 반복 호출해서 사용할 수 있다는 장점이 있습니다. 생성된 저장 프로시저를 제거하기 위해서는 DROP PROCEDURE 다음에 제거하고자 하는 프로시저 이름을 기술합니다. OR REPLACE 옵션은 이미 학습한 대로 이미 같은 이름으로 저장 프로시저를 생성할 경우 기존 프리시져는 삭제하고 지금 새롭게 기술한 내용으로 재 생성하도록 하는 옵션입니다.   

   - CREATE Procedure   
      -CREATE OR REPLACE 사용시 동일 이름의 Procedure를 덮어씀   
      -삭제시 DROP Procedure   
   - Mode   
      -IN : 운영체제에서 프로시저로 전달되는 변수( __default__ )   
      -OUT : 프로시저에서 운영체제로 전달되는 변수   
      -INOUT : 거의 사용하지 않음   
   - /
      -프로시저 컴파일 시작   
         
   ```
      CREATE [OR REPLACE] Procedure [Prcedure_name]
      (argument1 [mode] data_type1, argument2 [mode] data_type2, ...)
      IS ...
      BEGIN  ...
         EXCEPTION  ...
      END;
      /
   ```

   실행
   ```
      EXECUTE pro;
      EXE pro
   ```   

1. # 입출력이 없는 프로시져
   ```sql
      CREATE OR REPLACE PROCEDURE DEL_ALL
      IS
      BEGIN
         DELETE FROM EMP01;
      END;

      SELECT * FROM USER_SOURCE;    -- 프로시져 목록 확인

      EXEC DEL_ALL;                 -- 프로시져 실행
   ```   

1. # 입력이 있는 프로시져
   ```SQL      
      CREATE OR REPLACE PROCEDURE DEL_NAME(VNAME IN EMP01.ENAME%TYPE)
      IS
      BEGIN
         DELETE FROM EMP01 WHERE ENAME = VNAME;
      END;

      SELECT * FROM USER_SOURCE;    -- 프로시저 목록 확인

      EXEC DEL_NAME('SCOTT');       -- 프로시져 실행
   ```

1. # 입출력이 있는 프로시져
   ```SQL
      CREATE OR REPLACE PROCEDURE SAL_EMPNO(
         VEMPNO IN EMP.EMPNO$TYPE
         VENAME OUT EMP.E
      )
   ```

1. # Procedure 사용 예
   프로시저 생성   
   ```
      CREATE OR REPLACE PROCEDURE p_dept_insert(v_deptno IN NUMBER, v_dname IN VARCHAR2, v_loc IN VARCHAR2, v_result OUT VARCHAR2)
      IS
         cnt NUMBER := 0;
      BEGIN
         SELECT COUNT(*) INTO cnt
         FROM DEPT
         WHERE DEPTNO = v_deptno;
         
         if cnt > 0 then
            v_result := '이미 등록된 부서번호'
         else
            INSERT INTO DEPT(DEPTNO, DNAME, LOC) VALUES(v_deptno, v_dname, v_loc);
            COMMIT;
            v_result := '입력 완료';
      EXCEPTION
         WHEN OTHERS THEN
            ROLLBACK;
            v_result := 'ERROR 발생'
      END;
      /
   ```   

   실행 : 10번 부서를 등록   
   ```
      variable rslt varchar2(30);

      EXECUTE p_dept_insert(10,'dev','seoul',:rslt);
      print rslt;

      RSLT
      -----------------------
      이미 등록된 부서번호
      

      EXECUTE p_dept_insert(50,'dev','seoul',:rlslt);
      ptint rslt;

      RSLT
      -----------------------
      입력 완료
   ```   


   