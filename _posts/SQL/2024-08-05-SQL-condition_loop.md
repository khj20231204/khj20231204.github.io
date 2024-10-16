---
layout: single
title: 조건문과 반복문
categories: ORACLE
tag:
---

1. # 조건문
   기본적으로 모든 문장들은 나열된 순서대로 순차적으로 수행됩니다. 하지만 경우에 따라서는 문장의 흐름을 변경할 필요가 있습니다. 이때 사용하는 것이 IF문입니다. IF문은 조건을 제시해서 만족하느냐 하지 않느냐에 따라 문장을 선택적으로 수행하기 때문에 선택문이라고 합니다. 오라클에서는 3가지 형태의 선택문이 제공됩니다.   

1. # IF - THEN - END IF
   ```SQL
      IF condition THEN -- 조건문
         statements;       -- 실행할 문자
      END IF
   ```   

   예제1)   
   ```SQL
      --1. if  ~  then   ~ end if 
      --Q1. 사원테이블(EMP)에서 SCOTT 사원의 부서번호를 검색해서, 부서명을 출력하는
      --    PL/SQL문을 작성 하세요?

      SET SERVEROUTPUT ON
      DECLARE
         VEMPNO NUMBER(4);
         VENAME VARCHAR2(20);
         VDEPTNO DEPT.DEPTNO%TYPE;
         VDNAME VARCHAR2(20) := NULL;
      BEGIN
         SELECT EMPNO, ENAME, DEPTNO INTO VEMPNO, VENAME, VDEPTNO FROM EMP
            WHERE ENAME='SCOTT';

         IF VDEPTNO = 10 THEN
            VDNAME := 'ACCOUNTING';
         END IF;
         IF VDEPTNO = 20 THEN
            VDNAME := 'RESEARCH';
         END IF;
         IF VDEPTNO = 30 THEN
            VDNAME := 'SALES';
         END IF;
         IF VDEPTNO = 40 THEN
            VDNAME := 'OPERATIONS';
         END IF;
         
         DBMS_OUTPUT.PUT_LINE('사번  /  이름  /  부서명');
         DBMS_OUTPUT.PUT_LINE('-----------------------');
         DBMS_OUTPUT.PUT_LINE(VEMPNO || '/' || VENAME || '/' || VDNAME);
      END;
   ```   

   예제2)   
   ```SQL
      --Q2. 사원 테이블에서 SCOTT 사원의 연봉을 구하는 PL/SQL문 작성?
      SET SERVEROUTPUT ON
      DECLARE                     -- %ROWTYPE: EMP테이블의 8개 컬럼의 자료형을
                                 --           모두 참조한다는 의미를 가지고 있다. 
         VEMP EMP%ROWTYPE;       -- 레퍼런스 변수
         ANNSAL NUMBER(7,2);     -- 스칼라 변수
      BEGIN
         SELECT * INTO VEMP FROM EMP WHERE ENAME = 'SCOTT';

         IF VEMP.COMM IS NULL THEN
            VEMP.COMM := 0;
         END IF;
         
         ANNSAL := VEMP.SAL * 12 + VEMP.COMM;  -- 연봉
         
         DBMS_OUTPUT.PUT_LINE('사번  /  이름  / 연봉');
         DBMS_OUTPUT.PUT_LINE('--------------------');
         DBMS_OUTPUT.PUT_LINE(VEMP.EMPNO||'/'||VEMP.ENAME||'/'||ANNSAL); 
      END;
   ```

1. # IF - THEN - ELSE - END IF
   예제)   
   ```SQL
      --Q. 사원 테이블에서 SCOTT 사원의 연봉을 구하는 PL/SQL문 작성?
      SET SERVEROUTPUT ON
      DECLARE
         VEMP EMP%ROWTYPE;       -- 레퍼런스 변수
         ANNSAL NUMBER(7,2);     -- 스칼라 변수
      BEGIN
         SELECT * INTO VEMP FROM EMP WHERE ENAME='SCOTT';

         IF VEMP.COMM IS NULL THEN
            ANNSAL := VEMP.SAL * 12;
         ELSE
            ANNSAL := VEMP.SAL * 12 + VEMP.COMM;
         END IF;   
         
         DBMS_OUTPUT.PUT_LINE('사번  /  이름  /  연봉');
         DBMS_OUTPUT.PUT_LINE('---------------------');
         DBMS_OUTPUT.PUT_LINE(VEMP.EMPNO||'/'||VEMP.ENAME||'/'||ANNSAL);
      END;
   ```   

   1. # IF ~ THEN ~ ELSIF ~ ELSE ~ END IF
   ```SQL
      --Q. SCOTT 사원의 부서번호를 이용해서 부서명을 구하는 PL/SQL문 작성?
      SET SERVEROUTPUT ON
      DECLARE
         VEMP EMP%ROWTYPE;       --레퍼런스 변수
         VDNAME VARCHAR2(14);    --스칼라 변수
      BEGIN
         SELECT * INTO VEMP FROM EMP WHERE ENAME='SCOTT';
         
         IF VEMP.DEPTNO = 10 THEN
            VDNAME := 'ACCOUNTING';
         ELSIF VEMP.DEPTNO = 20 THEN
            VDNAME := 'RESEARCH';
         ELSIF VEMP.DEPTNO = 30 THEN
            VDNAME := 'SALES';
         ELSIF VEMP.DEPTNO = 40 THEN
            VDNAME := 'OPERATIONS';
         END IF;  
         
         DBMS_OUTPUT.PUT_LINE('사번 / 이름 / 부서명');
         DBMS_OUTPUT.PUT_LINE('------------------');
         DBMS_OUTPUT.PUT_LINE(VEMP.EMPNO||'/'||VEMP.ENAME||'/'||VDNAME);
      END;
   ```

1. # 반복문
   반복문은 SQL문을 반복적으로 여러 번 실행하고자 할 때 사용합니다. PL/SQL에서는 다양한 반복문이 사용됩니다.   
   1.조건 없이 반복 작업을 제공하기 위한 __BASIC LOOP문__   
   2.COUNT를 기본으로 작업의 반복 제어를 제공하는 __FOR LOOP문__   
   3.조건을 기본으로 작업의 반복 제어를 제공하기 위한 __WHILE LOOP문__   
   4.LOOP를 종료하기 위한 EXIT문   

   기본 문법
   
   ```SQL
      DECLARE
         변수 선언
      BEGIN
         LOOP
            statement;

            IF [CONDITION] THEN
               EXIT
            END IF

         END LOOP
      END;
   ```   
   END LOOP에 도달하면 이와 짝을 이루는 LOOP로 되돌아갑니다. PL/SQL에서 반복문의 기본은 무한 루프입니다. 이를 빠져나오기 위해서 `EXIT 조건`을 두게 됩니다.   

1. # BASIC LOOP
   ```SQL
      --1.BASIC LOOP문
      --  LOOP
      --      반복 실행될 문장;
      --      조건식   EXIT;
      --  END LOOP;

      --Q1. BASIC LOOP문으로 1 ~ 5까지 출력?
      SET SERVEROUTPUT ON
      DECLARE
         N NUMBER := 1;      --N변수의 초기값을 1로 설정
      BEGIN
         LOOP
            DBMS_OUTPUT.PUT_LINE(N);
            N := N + 1;
            IF N > 1000000 THEN
                  EXIT;     -- LOOP문을 빠져 나옴
            END IF;
         END LOOP;
      END;

      --ORA-20000: ORU-10027: BUFFER OVERFLOW, LIMIT OF 1000000 BYTES

      --Q2. 1부터 10까지 합을 구하는 프로그램을 작성?
      DECLARE
         N NUMBER := 1;    -- 루프를 돌릴 변수
         S NUMBER := 0;    -- 합이 누적될 변수  
      BEGIN
         LOOP
            S := S + N;   -- S변수에 합을 누적  
            N := N + 1;
            IF N > 10 THEN
                  EXIT;
            END IF;
         END LOOP;
         DBMS_OUTPUT.PUT_LINE('1~10까지의 합:' || S);
      END;
   ```   

1. # FOR LOOP
   ```SQL      
      --2. For Loop문
      --  FOR  변수  IN [REVERSE] 작은값..큰값 LOOP
      --     반복 실행될 문장;
      --  END  LOOP;

      --Q1. FOR LOOP문으로 1부터 5까지 출력?
      BEGIN
         FOR  N  IN  1..5  LOOP          --자동으로 1씩 증가
            DBMS_OUTPUT.PUT_LINE(N);
      --      N := N + 2;                 -- 2씩 증가(오류발생)
         END LOOP;
      END;

      --Q2. FOR LOOP문으로 5부터 1까지 출력?
      BEGIN
         FOR  N  IN REVERSE 1..5  LOOP          --자동으로 1씩 감소
            DBMS_OUTPUT.PUT_LINE(N);
         END LOOP;
      END;

      --Q3. FOR LOOP문을 이용해서 부서테이블(DEPT)의 모든 정보를 출력하는 PL/SQL문 작성?
      DECLARE
         VDEPT  DEPT%ROWTYPE;        --레퍼런스 변수
      BEGIN
         DBMS_OUTPUT.PUT_LINE('부서번호  /  부서명  /  지역명');
         FOR CNT IN 1..4 LOOP
            SELECT * INTO VDEPT FROM DEPT WHERE DEPTNO = 10 * CNT;
            
      DBMS_OUTPUT.PUT_LINE(VDEPT.DEPTNO||'/'||VDEPT.DNAME||'/'||VDEPT.LOC);
         
         END LOOP;
      END;
   ```   

1. # WHILE LOOP문
   ```SQL
      --   WHILE  조건식  LOOP
      --      반복 실행될 문장;
      --   END LOOP;

      --Q1. WHILE LOOP 문으로 1부터 5까지 출력?
      DECLARE
         N NUMBER := 1;      -- N변수의 초기값을 1로 설정
      BEGIN
         WHILE  N<=5 LOOP
            DBMS_OUTPUT.PUT_LINE(N);
            N := N + 1;
         END LOOP;
      END;

      --Q2. WHILE LOOP문으로 별(*)을 삼각형 모양으로 출력?
      DECLARE
         C NUMBER := 1;
         STAR VARCHAR2(100) := '';
      BEGIN
         WHILE C <= 10 LOOP
            STAR := STAR || '*';
            DBMS_OUTPUT.PUT_LINE(STAR);
            C := C + 1;
         END LOOP;
      END;   
   ```