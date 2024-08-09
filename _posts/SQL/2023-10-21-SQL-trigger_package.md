---
layout: single
title: 패키지와 트리거
categories: SQL
tag: [PL SQL]
---

1. # 패키지
   패키지 사전적인 의미는 꾸러미입니다. 관련 있는 프로시저를 보다 효율적으로 관리하기 위해서 패키지 단위로 배포할 때 유용하게 사용됩니다. 패지키는 패키지 선언(명세부)과 패키지 몸체 선언(몸체부) 두 가지 모두를 정의해야 합니다.   

   문법   
   ```SQL
      CREATE OR REPLACE PACKAGE 패키지명
      IS
         함수나 프로시저 선언
      END;

      CREATE OR REPLACE PACKAGE BODY 패키지명
      IS
         함수나 프로시저 정의
      END;
   ```   

   ```SQL
      -- 패키지(PACKAGE):저장 프로시저와 저장 함수를 묶어 놓은 것.
      -- 패키지 = 패키지 헤드 + 패키지 바디

      -- 패키지 생성
      -- 1. 패키지 헤드 생성
      CREATE OR REPLACE PACKAGE EXAM_PACK
      IS
         FUNCTION CAL_BONUS(VEMPNO IN EMP.EMPNO%TYPE)    -- 저장함수
         RETURN NUMBER;
         PROCEDURE CURSOR_SAMPLE02;
      END;
      -- 2. 패키지 바디 생성
      CREATE OR REPLACE PACKAGE BODY EXAM_PACK
      IS 
         -- 저장함수 : CAL_BONUS
         function cal_bonus(vempno in emp.empno%type)
            return number                  -- 돌려줄 값의 자료형
         is
            vsal number(7,2);              -- 로컬변수
         begin
            select sal into vsal from emp where empno = vempno;
            return vsal * 2;              -- 200% 인상한 급여를 돌려준다. 
         end;
         
         -- 저장 프로시져 : CURSOR_SAMPLE02
         PROCEDURE CURSOR_SAMPLE02
         IS
            VDEPT DEPT%ROWTYPE; --로컬 변수생성 
            CURSOR C1
            IS 
            SELECT * FROM DEPT;
         BEGIN
            dbms_output.put_line('부서번호  /  부서명  /  지역명');
            dbms_output.put_line('---------------------------');
            FOR VDEPT IN C1 LOOP
                  EXIT WHEN C1%NOTFOUND;
                  dbms_output.put_line(vdept.deptno||'/'||vdept.dname||'/'||vdept.loc);        
            END LOOP;
         END;
      END;

      SELECT * FROM USER_SOURCE;

      -- 3.저장 프로시져
      EXECUTE EXAM_PACK.cursor_sample02;
         
      -- 4. 저장 함수 실행 : CAL_BONUS()
      -- 1)바인드 변수 생성
      VARIABLE VAR_RES NUMBER;

      -- 2)실행
      EXECUTE :VAR_RES := EXAM_PACK.CAL_BONUS(7788);

      PRINT VAR_RES;

      SELECT ENAME, EXAM_PACK.CAL_BONUS(7788) FROM EMP WHERE EMPNO=7900;
      SELECT ENAME, EXAM_PACK.CAL_BONUS(7788) FROM EMP WHERE EMPNO=7788;
   ```   

1. # 트리거(Trigger)
   트리거의 사전적 의미?   
   ①(총의)방아쇠 = HIR TRIGGER   
   ②제동기, 제륜 장치   
   ③(연쇄 방응, 생리 현상, 일련의 사건등을 유발하는) 계기, 유인, 자극   

   오라클에서 트리거 역시 해당 단어의 의미처럼 어떤 이벤트가 발생하면 자동적으로 방아쇠가 당겨져 총알이 발사되듯이 특정 테이블이 변경되면 이를 이벤트로 다른 테이블이 자동으로 변경되도록 하기 위해서 사용합니다. 트리거는 특정 동작을 이벤트로 인해서만 실행되는 프로시저의 일종입니다.   

   1)트리거의 타이밍   
   `[BEFORE]`   
   타이밍은 어떤 테이블에 INSERT, UPDATE, DELETE문이 실행될 때 해당 문장이 __실행되기 전__ 에 트리거가 가지고 있는 BEGIN ~ END 사이의 문장을 실행합니다.   

   `[AFTER]`   
   타이밍은 INSERT, UPDATE, DELETE문이 __실행된 후__ 에 트리거가 가지고 있는 BEGIN ~ END 사이의 문장을 실행합니다.  

   2)트리거의 이벤트   
   사용자가 어떤 DML(INSERT, UPDATE, DELETE)문을 실행했을 때 트리거를 발생시킬 것인지를 결정합니다.   

   3)트리거의 몸체   
   해당 타이밍에 해당 이벤트가 발생하게 되면 실행될 기본 로직이 포함되는 부분으로 BEGIN ~ END에 기술합니다.   

1. # 트리거의 유형
   트리거의 유형은 FOR EACH ROW에 의해 문장 레벨 트리거와 행 레벨 트리거로 나눕니다.   
   FOR EACH ROW가 생략되면 문장 레벨 트리거이고 행 레벨 트리거를 정의하고자 할 때에는 반드시 FOR EACH ROW를 기술해야 합니다.   

   ```
      FOR EACH ROW - 행 레벨 트리거   
      FOR EACH ROW 생략 - 문장 레벨 트리거   
   ```   

   문장 레벨 트리거는 어떤 사용자가 트리거가 설정되어 있는 테이블에 대해 DML(INSERT, UPDATE, DELETE)문을 실행할 때 단 한번만 트리거를 발생시킬 때 사용합니다.   
   행 레벨 트리거는 DML(INSERT, UPDATE, DELETE)문에 의해서 여러 개의 행이 변경된다면 각 행이 변결될 때마다 트리거를 발생시키는 방법입니다. 만약 5개의 행이 변경되면 5번 트리거가 발생됩니다.   
   DML문 수행 시 연결된 동작을 자동으로 수행하도록 작성된 프로그램으로 사용자가 명시적으로 호출하지 않으며, 조건이 맞으면 __자동으로 수행__ 됩니다.   
   
   Procedure는 Execute 명령어로 실행하고, Function는 함수 이름으로 실행하지만 Trigger는 생성된 후 DML에 의해 자동으로 실행됩니다.   
   - 주로 데이터 무결성 보장을 위해 FK처럼 동작하거나, 실시간 집계성 테이블 생성에 사용됨   
   - 보안 적용, 유해하지 않은 트랜잭션 예방, 업무 규칙 적용, 감사 제공 등에서 사용   
   - OLTP 시스템에서는 부하로 인해 성능이 저하될 수 있음   
   - ROLLBACK 시, 원 트랜잭션 뿐 아니라 Trigger에 의해 실행된 연산도 __모두 취소됨__   
      -Trigger는 INSERT, UPDATE, DELETE문과 연결된 하나의 트랜잭션 내에서 수행되는 작업으로 이해해야 함   
      -Procedure : Begin ~ End 사이에 COMMIT, ROLLBACK 사용 가능   
      -Trigger : Begin ~ End 사이에 COMMIT, ROLLBACK 사용 불가   
   - Row Trigger와 Statement Trigger로 구분   

1. # 트리거 주요 구문
   - FOR EACH ROW   
      -Row Trigger / Statement Trigger의 지정을 위한 구문   
      -"FOR EACH ROW" 사용 → Row Level Trigger → SQL문장의 각 행마다 Trigger 발생   
      -"FOR EACH ROW" 생략 → Statement Level Trigger → SQL 한 문장에 한 번만 Trigger 발생   
   <img src="../../imgs/sql/trigger_row_statement.png" style="boder:3px solid black;boder-radius:9px;width:600px">   

   - AFTER / BEFORE   
      -Trigger 수행 시점 명시   
   - :NEW / :OLD   
      -:NEW는 문장 수행 후의 정보를 갖는 구조체   
      ex)o_prod := :NEW.product   
      -:OLD는 문장 수행 전의 정보를 갖는 구조체      
   <img src="../../imgs/sql/trigger_new_old.png" style="boder:3px solid black;boder-radius:9px;width:500px">   
   - 변수 선언   
      -ORDER.order_date%TYPE;   
      → ORDER테이블의 order_date컬럼과 동일한 타입으로 선언   

1. # 트리거 생성 예
   ```SQL
      -- 트리거(TRIGGER)
      -- 1.트리거의 사전적인 의미는 방아쇠라는 의미를 가지고 있다
      -- 2.트리거는 이벤트를 발생 시켜서 연쇄적으로 다른 작업을 자동으로 수행
      -- 3.이벤트는 DML SQL문을 이용해서 이벤트를 발생시키고, 이때 연쇄적으로 실행부(BEGIN ~ END)
      --  안의 내용을 자동으로 실행시켜준다.

      -- Q1.사원테이블에 사원이 등록되면, "신입 사원이 입사 했습니다."라는 메세지를 출력하는 트리거를 생성하라

      -- 1.예제로 적용할 사원 테이블 생성
      DROP TABLE EMP01 PURGE;
      CREATE TABLE EMP01(
         EMPNO NUMBER(4) PRIMARY KEY,
         ENAME VARCHAR2(20),
         JOB VARCHAR2(20)
      );

      SELECT * FROM TAB;

      -- 2.트리거 생성
      CREATE OR REPLACE TRIGGER TRG_01
         AFTER INSERT ON EMP01 -- EMP01 테이블에 INSERT가 된 다음에! 라는 의미 : 이벤트 발생
      BEGIN
         DBMS_OUTPUT.PUT_LINE('신입사원이 입사했다');
      END;

      -- 3.트리거 목록 확인
      SELECT * FROM USER_TRIGGERS;

      -- 4.이벤트 발생 : EMP01 테이블에 회원가입(데이터 입력)
      SET SERVEROUTPUT ON
      DESC EMP01;
      INSERT INTO EMP01 VALUES(1,'ONE_MEMBER','SALES');
      INSERT INTO EMP01 VALUES(2,'TWO_MEMBER','MANAGER');
      SELECT * FROM EMP01;

      -- Q2.사원테이블(EMP01)에 신입 사원이 등록되면, 급여 테이블(SAL01)에 급여를 자동으로 추가해주는 트리거를 생성하라

      -- 1. 사원 테이블 : EMP01
      DELETE FROM EMP01;
      COMMIT;

      -- 2. 급여 테이블 생성
      CREATE TABLE SAL01(
         SALNO NUMBER(4) PRIMARY KEY, -- 기본키(PRIMARY KEY)
         SAL NUMBER(7,2), 
         EMPNO NUMBER(4) REFERENCES EMP01(EMPNO)
      );

      SELECT * FROM TAB;

      -- 3.시퀀스 생성
      CREATE SEQUENCE SAL01_SALNO_SEQ;   --1부터 1씩 증가되는 시퀀스 생성

      SELECT * FROM SEQ;
      SELECT * FROM USER_SEQUENCES;

      -- 4.트리거 생성
      -- :NEW.컬럼명 : INSERT, UPDATE문을 이용해서 이벤트가 발생한 경우
      -- :OLD.컬럼명 : DELETE문을 이용해서 이벤트가 발생한 경우
      CREATE OR REPLACE TRIGGER TRG_02
         AFTER INSERT ON EMP01   -- 이벤트 생성
         FOR EACH ROW            -- 행레벨 트리거
      BEGIN
         INSERT INTO SAL01 VALUES(SAL01_SALNO_SEQ.NEXTVAL, 300, :NEW.EMPNO);
      END;
      -- EMP01에 INSERT가 일어나면 BEGIN ~ END; 구문 안에 있는 INSERT INTO ~ 를 실행

      -- 5.트리거 목록 확인
      SELECT * FROM USER_TRIGGERS;

      -- 6.이벤트 발생 : EMP01 테이블에 데이터 입력
      INSERT INTO EMP01 VALUES(1111,'홍길동','개발자');
      INSERT INTO EMP01 VALUES(1112,'홍길순','화가');

      -- 7.데이터 확인
      SELECT * FROM EMP01;
      SELECT * FROM SAL01;

      -- Q3.사원 테이블(EMP01)에서 사원정보가 삭제되면, 급여 테이블(SAL01)의 정보를 자동으로 삭제하는 트리거를 생성
      DELETE FROM EMP01 WHERE EMPNO=1111;

      CREATE OR REPLACE TRIGGER TRG_03
         AFTER DELETE ON EMP01   -- 이벤트 발생
         FOR EACH ROW            -- 행레벨 트리거
      BEGIN
         DELETE FROM SAL01 WHERE EMPNO = :OLD.EMPNO;
      END;
      -- EMP01테이블에 DELETE가 발생하면 BEING ~ END; 사이에 명령어 실행

      -- 2.트리거 목록 확인
      SELECT * FROM USER_TRIGGERS;

      -- 3.이벤트 발생
      -- : 사원 테이블(EMP01)의 사원번호 1111번 사원을 삭제(탈퇴)하면, 연쇄적으로 
      -- 급여 테이블(SAL01)의 급여 정보도 같이 삭제된다.
      DELETE FROM EMP01 WHERE EMPNO=1111;

      SELECT * FROM EMP01;
      SELECT * FROM SAL01;
   ```   

   예제2)   
   ```SQL
      REATE OR REPLACE TRIGGER summary_sales
      AFTER INSERT  /* 3)INSERT 이후에 트리거를 발생 시켜라 */
      ON ORDER  /* 1)ORDER 테이블에 대해서*/
      FOR EACH ROW  /* 2)문장 전체가 아니라 한행 한행 각각 마다 트리거 발생하는데  */

      DECLARE
         o_date ORDER.order_date%TYPE;  /* o_date변수를 선언하는데 ORDER테이블에 있는 order_date컬럼의 타입과 같은 타입으로 만듦*/
         o_prod ORDER.product%TYPE;  /* o_prod변수를 선언하는데 ORDER테이블에 있는 product컬럼의 타입과 같은 타입으로 만듦 */

      BEGIN
         o_date := :NEW.order_date; /* order_date에 새로운 값이 입력되면 o_date에 저장 */
         o_prod := :NEW.product;  /* product에 새로운 값이 입력되면 o_prod에 저장 */
         UPDATE SALES SET qty = qty + :NEW.qty, amount = amount + :NEW.amount
         /* qty(sales테이블의 qty) + :NEW.qty(ORDER테이블의 INSERT 후의 qty) */
         /* amount(sales테이블의 amount) + :NEW.amount(ORDER테이블의 INSERT 후의 amount) */
         WHERE sale_date = o_date AND product = o_prod;

         IF SQL%NOTFOUND THEN   
         /* update시 기존 데이터가 있어야 업데이트가 가능한데 기존 데이터가 없을 시 최초 한번은 입력을해야 함, 
         업데이트 할 기존 데이터가 없으면 실행 됨 */
            INSET INTO SALES VALUES(o_date, o_prod, :NEW.qty, :NEW.amount);
         END IF;
      END;  
         /
   ```