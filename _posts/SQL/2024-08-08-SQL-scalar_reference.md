---
layout: single
title: 스칼라 변수/레퍼런스 변수
categories: SQL
tag: []
---

1. # 스칼라 변수
   PL/SQL에서 변수를 선언할 때 사용되는 자료형은 SQL에서 사용하던 자료형과 거의 유사합니다. 숫자를 저장하려면 NUMBER를 사용하고 문자를 저장하려면 VARCHAR2를 사용해서 선언합니다.   
   ```SQL
      VEMPNO NUMBER(4);
      VENAME VARCHAR2(10);
   ```   

1. # 레퍼런스 변수
   이미 선언되어 있는 다른 변수 또는 데이터베이스 컬럼에 맞추어 변수를 선언하기 위해 %TYPE 속성을 사용할 수 있습니다.   
   ```SQL
      VEMPNO EMP.EMPNO%TYPE; --EMP테이블에 EMPNO컬럼의 데이터 타입을 가져온다
      VENAME EMP.ENAME%TYPE; --EMP테이블에 ENAME컬럼의 데이터 타입을 가져온다
   ```   

1. # 변수 사용 예 
   PL/SQL 변수 사용 예제
   ```SQL         
      SET SERVEROUTPUT ON
      DECLARE
         VEMPNO NUMBER(4);
         VENAME VARCHAR2(20);
         VDEPTNO EMP.DEPTNO%TYPE;   -- EMP테이블에 DEPTNO컬럼의 데이터타입
         VDNAME VARCHAR2(20) := NULL; -- VDNAME변수에 NULL대입
      BEGIN
         SELECT EMPNO, ENAME, DEPTNO INTO VEMPNO, VENAME, VDEPTNO
         FROM EMP
         WHERE EMPNO = 7788;

         IF VDEPTNO = 10 THEN
            VDNAME := '10'
         END IF
         
         DBMS_OUTPUT.PUT_LINE(VEMPNO || VENAME || VDNAME);  -- DBMS_OUTPUT.PUT_LINE로 출력
      END;
   ```   

1. # 행 단위 참조 ROWTYPE
   %TYPE가 컬럼 단위로 참조한다면 로우(행) 단위로 참조하는 %ROWTYPE가 있습니다.   
   데이터베이스의 테이블 또는 VIEW의 일련의 컬럼을 RECORD로 선언하기 위하여 %ROWTYPE를 사용합니다.   
   데이터베이스 테이블 이름을 %ROWTYPE 앞에 접두어를 붙여 RECORD를 선언하고 FIELD는 테이블이나 VIEW의 COLUMN명과 데이터 타입과 LENGTH을 그대로 가져올 수 있습니다.   
   ```SQL
      VEMP EMP%ROWTYPE;
   ```   

1. # ROWTYPE 사용예
   ```SQL
      SET SERVEROUTPUT ON
      DECLARE
         VEMP EMP%ROWTYPE; --EMP테이블의 모든 컬럼 타입을 가져옴
      BEGIN
         SELECT * INTO VEMP FROM EMP WHERE ENAME='SCOTT';

         DBMS_OUTPUT.PUT_LINE(VEMP.EMPNO || VEMP.ENAME);
      END;
   ```