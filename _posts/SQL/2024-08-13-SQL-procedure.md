---
layout: single
title: 프로시저와 저장 함수
categories: ORACLE
tag: [cross, 레코드 수 문제]
---

1. # Procedure(프로시저)
   함수 (Function): 반드시 하나의 값을 반환해야 합니다. 이 반환값은 SQL 문에서 다른 값처럼 사용될 수 있습니다.   
   저장 프로시저 (Procedure): 반환값이 없거나, OUT 파라미터를 통해 여러 값을 반환할 수 있습니다.   

   저장 프로시저를 생성하려면 CREATE PROCEDURE다음에 새롭게 생성하고자하는 프로지셔 이름을 기술합니다. 이렇게 해서 생성한 저장 프로시저는 여러 번 반복 호출해서 사용할 수 있다는 장점이 있습니다. 생성된 저장 프로시저를 제거하기 위해서는 DROP PROCEDURE 다음에 제거하고자 하는 프로시저 이름을 기술합니다. OR REPLACE 옵션은 이미 학습한 대로 이미 같은 이름으로 저장 프로시저를 생성할 경우 기존 프리시져는 삭제하고 지금 새롭게 기술한 내용으로 재 생성하도록 하는 옵션입니다.   

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

   *DBMS.OUTPUT.PUT_LINE('-----');해석   
   DBMS.OUTPTU : 패키지   
   PUT_LINE : 저장 프로시저   

1. # SET SERVEROUTPUT ON
   EXECUTE pro;나 EXE pro;를 실행했는데 실행 결과가 나타나지 않을 때 'SET SERVEROUTPUT ON' 명령을 실행합니다.   
   Oracle 데이터베이스에서 PL/SQL 블록 내에서 출력을 화면에 표시하기 위해 사용하는 명령입니다.   


1. # 입출력이 없는 프로시저

   ```sql
      -- 1.저장 프로시저 생성
      CREATE OR REPLACE PROCEDURE DEL_ALL
      IS 
      BEGIN
         DELETE FROM EMP01;
      END;

      -- 2.프로시저 목록 확인
      SELECT * FROM USER_SOURCE;

      -- 3.프로시저 실행
      EXEC DEL_DALL;
      EXECUTE DEL_DALL;

      -- 4.프로시저 실행 결과 확인
      SELECT * FROM EMP01;

      -- 5.ROLLBACK;
      ROLLBACK;

      SET AUTOCOMMIT OFF

      -- 6.테이블에 데이터 입력
      INSERT INTO EMP01 SELECT * FROM EMP;
   ```   

1. # 입력이 있는 프로시저   

   ```SQL      
      -- 매개변수가 있는 프로시저
      -- 매개변수의 MODE값 
      -- IN : 매개변수로 값을 받는 역할
      -- OUT : 매개변수로 값을 돌려주는 역할

      -- 1. 매개변수가 있는 프로시저 생성
      CREATE OR REPLACE PROCEDURE DEL_ENAME(VENAME IN EMP01.ENAME%TYPE)
      IS
      BEGIN
         DELETE FROM EMP01 WHERE ENAME = VENAME;
      END;

      -- 2.프로시저 목록 확인
      SELECT * FROM USER_SOURCE;

      -- 3.프로시저 실행
      EXEC DEL_ENAME('SCOTT');
      EXECUTE DEL_ENAME('SMITH');

      -- 4.목록 확인
      SELECT * FROM EMP01;

      -- 5.ROLLBACK
      ROLLBACK;
   ```

1. # 입출력이 있는 프로시저   

   예1)   

   ```SQL
      -- 매개변수의 MODE가 IN, OUT으로 되어있는 프로시저 생성
      -- IN : 매개변수로 값을 받는 역할
      -- OUT : 매개변수로 값을 돌려주는 역할

      -- Q.프로시저의 매개변수에 사원번호를 전달해서 그 사원의 사원명, 급여, 직책을 구하는 프로시저
      SELECT * FROM EMP01;
      CREATE OR REPLACE PROCEDURE SAL_EMPNO(
         VEMPNO IN EMP01.EMPNO%TYPE,  --사원번호
         VENAME OUT EMP01.ENAME%TYPE, --사원명
         VSAL OUT EMP01.SAL%TYPE,     --급여
         VJOB OUT EMP01.JOB%TYPE      --직책
         )
      IS
      BEGIN
         SELECT ENAME, SAL, JOB INTO VENAME, VSAL, VJOB FROM EMP01 
         WHERE EMPNO = VEMPNO;
      END;

      -- 2.프로시저 확인
      SELECT * FROM USER_SOURCE;

      -- 3.바인드 변수 : 프로시저를 실행할 때 결과를 돌려받는 변수
      VARIABLE VAR_ENAME VARCHAR2(12);
      VARIABLE VAR_SAL NUMBER;
      VARIABLE VAR_JOB VARCHAR2(10);

      -- 4.프로시저 실행
      EXECUTE SAL_EMPNO(7788, :VAR_ENAME, :VAR_SAL, :VAR_JOB);
      EXECUTE SAL_EMPNO(7839, :VAR_ENAME, :VAR_SAL, :VAR_JOB);

      -- 5.바인드 변수로 돌려받은 값을 출력
      PRINT VAR_ENAME;
      PRINT VAR_SAL;
      PRINT VAR_JOB;
   ```   
   프로시저를 생성하고 출력을 받을 변수를 생성합니다. 줄력 받을 변수는   
   ```s
      variable 변수명 데이터타입;
   ```   
   로 선언이 됩니다. execute로 프로시저를 실행할 때 출력 변수로 출력값을 받습니다. 이때 출력받는 값은 `:변수명` 으로 앞에 콜론을 붙이게됩니다.   
   이후 print로 변수 값을 출력합니다.   

   예2)   

   ```sql
      CREATE OR REPLACE PROCEDURE p_dept_insert(
         v_deptno IN NUMBER, 
         v_dname IN VARCHAR2, 
         v_loc IN VARCHAR2, 
         v_result OUT VARCHAR2)
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

   ```sql
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

1. # 저장 함수 생성
   저장 함수는 저장 프로시저와 거의 유사한 용도로 사용합니다. 차이점은 함수는 실행 결과를 되돌려 받을 수 있다는 점입니다.   

   프로시저를 만들 때에는 PROCEDURE라고 기술하지만, 함수를 만들 때에는 FUNCTION이라고 기술합니다. 함수는 결과를 되돌려 받기 위해서 함수가 되돌려 받게 되는 자료형과 되돌려 받을 값을 기술해야 합니다. 프로시저와 달리 __반드시 수행 결과값을 Return__ 해야하며, 프로시저는 매개변수로 받아온 OUT으로 선언한 변수에 return값을 넘기는데, 사용자 정의 함수는 RETURN으로 반드시 결과 값을 리턴해야합니다.   
   
   기본 문법   

   ```SQL
      CREATE [OR REPLACE] FUNCTION 함수명(변수명 IN 데이터타입, 변수명 OUT 데이터타입)
         RETURN 반환타입
      IS
         변수명 데이터타입 -- SELECT 결과값을 받을 변수명
      BEGIN
         
         STATEMENT;

         RETURN 반환값
      END;
      /
   ```   

   예제1)   

   ```SQL
      -- Q2.사원 테이블에서 사원명을 저장함수의 매개변수로 전달하여 해당 사원의 직급을 구해오는 저장함수를 생성하고 실행
      -- 1.저장 함수 생성
      CREATE OR REPLACE FUNCTION JOB_EMP(VENAME IN EMP.ENAME%TYPE)
         RETURN VARCHAR2     -- 돌려줄 값의 자료형
      IS  
         VJOB EMP.JOB%TYPE;  -- 로컬변수(사원명으로 검색한 사원의 JOB저장)
      BEGIN
         SELECT JOB INTO VJOB FROM EMP WHERE ENAME = VENAME;
         RETURN VJOB;
      END;
   ```   

   예제2)   

   ```SQL
      CREATE OR REPLACE FUNCTION CAL_BONUS(VEMPNO IN EMP.EMPNO%TYPE)
         RETURN NUMBER
      IS
         VSAL NUMBER(7,2); --7자리, 소수점아래 2자리
      BEGIN
         SELECT SAL INTO VSAL FROM EMP
         WHERE EMPNO = VEMPNO;
         
         RETURN (VSAL * 200);
      END;

      -- 2.저장함수 목록 확인
      SELECT * FROM USER_SOURCE;

      -- 3.바인드 변수 생성
      VARIABLE VAR_RES NUMBER;

      -- 4.저장함수 실행
      EXECUTE :VAR_RES := CAL_BONUS(7788);

      -- 5.바인드 변수의 돌려받은 결과값 출력
      PRINT VAR_RES;

      -- 저장함수를 SQL문에 포함 시켜서 실행
      SELECT ENAME, SAL, CAL_BONUS(7788) FROM EMP WHERE EMPNO=7788;
      SELECT ENAME, SAL, CAL_BONUS(7900) FROM EMP WHERE EMPNO=7900;
   ```   

   예제3)   
   
   ```SQL
      CREATE OR REPLACE FUNCTION JOB_EMP(VENAME IN EMP.ENAME%TYPE)
         RETURN VARCHAR2     -- 돌려줄 값의 자료형
      IS  
         VJOB EMP.JOB%TYPE;  -- 로컬변수(사원명으로 검색한 사원의 JOB저장)
      BEGIN
         SELECT JOB INTO VJOB FROM EMP WHERE ENAME = VENAME;
         RETURN VJOB;
      END;

      -- 2.저장 함수 목록 확인
      SELECT * FROM USER_SOURCE;

      -- 3.바인드 변수 생성
      VARIABLE VAR_JOB VARCHAR2(10);

      -- 4.저장함수 실행
      EXEC :VAR_JOB := JOB_EMP('SCOTT');
      EXEC :VAR_JOB := JOB_EMP('KING');

      -- 5.바인드 변수 결과값 출력
      PRINT VAR_JOB;

      -- 저장함수를 SQL문에 포함해서 실행
      SELECT ENAME, JOB_EMP('SCOTT') FROM EMP WHERE ENAME='SCOTT';
      SELECT ENAME, JOB_EMP('KING') FROM EMP WHERE ENAME='KING';
   ```   

1. # OUT 매개변수와 RETURN 문 비교
   
   함수의 목적: 함수의 본래 목적에 맞게 OUT 매개변수를 사용해야 합니다.   
   반환 값: OUT 매개변수 외에 추가적인 값을 반환해야 할 경우 RETURN 문을 사용합니다.   
   호출 시 변수 할당: OUT 매개변수는 함수 호출 시 변수를 할당해야 합니다.   

   OUT 매개변수 vs. RETURN 문   

   |        구분       |       OUT매개변수          |        RETURN 문         |
   |:-----------------:|:-------------------------:|:------------------------:|
   |        용도       | 여러 값 반환, 부가적인 작업 |         단일 값 반환      |
   |      사용시기     | 함수 호출 시 변수 할당 필요  |  함수 호출 시 반환 값 저장 |
   | 일반적인 사용 방식 |    함수의 부가적인 기능     |   함수의 주된 기능       |



   


   