---
layout: single
title: 자바에서 프로시저 사용
categories: SQL
tag: 
---

1. # 자바에서 오라클 프로시저 사용
   callableStatement를 이용합니다. callableStatement는 PreparedStatement의 하위 인터페이스로 SQL프로시저를 실행하는데 이용됩니다.   

   preparedCall(String sql) : 프로시저를 호출하는 CallableStatement 객체 생성   
   setInt(int ParameterIndex, int x) : IN파라미터 설정   
   setString(int ParameterIndex, String x) : IN파라미터 설정   
   registerOutParameter(int ParameterIndex, int sqlType) : OUT파라미터 등록   
   execute() : 실행

1. # 입출력이 없는 프로시저 실행
   ```sql
      CREATE OR REPLACE PROCEDURE DEL_ALL
      IS
      BEGIN
         DELETE FROM EMP01;
      END;
   ```   

   ```java
      public static void main(String[] args) {
         Connection con = null;
         String url = "jdbc:oracle:thin:@localhost:1521:xe";
         String sql = null;
         CallableStatement cs = null;

         try {
            Class.forName("oracle.jdbc.driver.OracleDriver");
            con = DriverManager.getConnection(url, "scott", "tiger");

            sql = "{call del_all()}";

            // CallableStatement를 객체를 생성
            cs = con.prepareCall(sql);
            cs.execute();
            System.out.println("프로시저 실행 성공");
            
            cs.close();
            con.close();
         } catch (Exception e) {
            System.out.println(e);
         }
      }
   ```

1. # 입력이 있는 프로시저 실행
   ```sql
      CREATE OR REPLACE PROCEDURE DEL_ENAME(VENAME IN EMP01.ENAME%TYPE)
      IS
      BEGIN
         DELETE FROM EMP01 WHERE ENAME = VENAME;
      END;
   ```

   ```java
      public static void main(String[] args) {
         Connection con = null;
         String url = "jdbc:oracle:thin:@localhost:1521:xe";
         String sql;
         CallableStatement cs = null;
         
         System.out.print("탈퇴할 회원명을 입력 하세요?");
         Scanner sc=new Scanner(System.in);
         String name = sc.next();
         
         try {
            Class.forName("oracle.jdbc.driver.OracleDriver");
            con = DriverManager.getConnection(url, "scott", "tiger");

            sql = "{call del_ename(?)}";

            // CallableStatement를 객체를 생성
            cs = con.prepareCall(sql);
            cs.setString(1, name);
            cs.execute();
            
            System.out.println("해당 데이터 삭제");
            
            cs.close();
            con.close();
         } catch (Exception e) {
            System.out.println(e);
         }
      }
   ```

1. # 입출력이 있는 프로시저 실행
   ```SQL
      CREATE OR REPLACE PROCEDURE SEL_CUSTOMER(
         VNAME IN CUSTOMER.NAME%TYPE,
         VEMAIL OUT CUSTOMER.EMAIL%TYPE,
         VTEL OUT CUSTOMER.TEL%TYPE)
      IS
      BEGIN
         SELECT EMAIL, TEL INTO VEMAIL, VTEL FROM CUSTOMER
         WHERE NAME = VNAME;
      END;
   ```

   ```JAVA
      public static void main(String[] args) {
         Connection con = null;
         String url = "jdbc:oracle:thin:@localhost:1521:xe";
         String sql;
         String name = "홍길동";
         CallableStatement cs = null;

         try {
            Class.forName("oracle.jdbc.driver.OracleDriver");
            con = DriverManager.getConnection(url, "scott", "tiger");

            sql = "{call sel_customer(?,?,?)}";

            // CallableStatement를 객체를 생성
            cs = con.prepareCall(sql);
            cs.setString(1, name);
            cs.registerOutParameter(2, java.sql.Types.VARCHAR);
            cs.registerOutParameter(3, java.sql.Types.VARCHAR);

            cs.execute();
            System.out.println("이름 \t 이메일 \t\t 전화번호   ");
            System.out.println("-----------------------------------------------");
            System.out.println(name + " \t " + cs.getString(2) + " \t " + cs.getString(3));

            cs.close();
            con.close();
         } catch (Exception e) {
            System.out.println(e);
         }
      }
   ```