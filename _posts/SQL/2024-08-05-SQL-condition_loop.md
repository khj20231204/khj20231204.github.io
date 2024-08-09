---
layout: single
title: 조건문과 반복문
categories: SQL
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
      declare
         vempno number(4);
         vename varchar2(20);
         vdeptno dept.deptno%type;
         vdname varchar2(20) := null;
      begin
         select empno, ename, deptno into vempno, vename, vdeptno from emp
            where ename='SCOTT';

         if vdeptno = 10 then
            vdname := 'ACCOUNTING';
         end if;
         if vdeptno = 20 then
            vdname := 'RESEARCH';
         end if;
         if vdeptno = 30 then
            vdname := 'SALES';
         end if;
         if vdeptno = 40 then
            vdname := 'OPERATIONS';
         end if;
         
         dbms_output.put_line('사번  /  이름  /  부서명');
         dbms_output.put_line('-----------------------');
         dbms_output.put_line(vempno || '/' || vename || '/' || vdname);
      end;
   ```   

   예제2)   
   ```SQL
      --Q2. 사원 테이블에서 SCOTT 사원의 연봉을 구하는 PL/SQL문 작성?
      set serveroutput on
      declare                     -- %rowtype: emp테이블의 8개 컬럼의 자료형을
                                 --           모두 참조한다는 의미를 가지고 있다. 
         vemp emp%rowtype;       -- 레퍼런스 변수
         annsal number(7,2);     -- 스칼라 변수
      begin
         select * into vemp from emp where ename = 'SCOTT';

         if vemp.comm is null then
            vemp.comm := 0;
         end if;
         
         annsal := vemp.sal * 12 + vemp.comm;  -- 연봉
         
         dbms_output.put_line('사번  /  이름  / 연봉');
         dbms_output.put_line('--------------------');
         dbms_output.put_line(vemp.empno||'/'||vemp.ename||'/'||annsal); 
      end;
   ```

1. # IF - THEN - ELSE - END IF
   예제)   
   ```SQL
      --Q. 사원 테이블에서 SCOTT 사원의 연봉을 구하는 PL/SQL문 작성?
      SET SERVEROUTPUT ON
      declare
         vemp emp%rowtype;       -- 레퍼런스 변수
         annsal number(7,2);     -- 스칼라 변수
      begin
         select * into vemp from emp where ename='SCOTT';

         if vemp.comm is null then
            annsal := vemp.sal * 12;
         else
            annsal := vemp.sal * 12 + vemp.comm;
         end if;   
         
         dbms_output.put_line('사번  /  이름  /  연봉');
         dbms_output.put_line('---------------------');
         dbms_output.put_line(vemp.empno||'/'||vemp.ename||'/'||annsal);
      end;
   ```   

   1. # if ~ then ~ elsif ~ else ~ end if
   ```SQL
      --Q. SCOTT 사원의 부서번호를 이용해서 부서명을 구하는 PL/SQL문 작성?
      SET SERVEROUTPUT ON
      declare
         vemp emp%rowtype;       --레퍼런스 변수
         vdname varchar2(14);    --스칼라 변수
      begin
         select * into vemp from emp where ename='SCOTT';
         
         if vemp.deptno = 10 then
            vdname := 'ACCOUNTING';
         elsif vemp.deptno = 20 then
            vdname := 'RESEARCH';
         elsif vemp.deptno = 30 then
            vdname := 'SALES';
         elsif vemp.deptno = 40 then
            vdname := 'OPERATIONS';
         end if;  
         
         dbms_output.put_line('사번 / 이름 / 부서명');
         dbms_output.put_line('------------------');
         dbms_output.put_line(vemp.empno||'/'||vemp.ename||'/'||vdname);
      end;
   ```
