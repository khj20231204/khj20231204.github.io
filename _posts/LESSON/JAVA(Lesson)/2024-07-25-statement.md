---
layout: single
title: 07_25.statement문으로 작성
categories: JAVA(Lesson)
tag: []
author_profile: false
---

1. # Select
   ```java
      public class JDBC_Select {

         public static void main(String[] args) {
            // TODO Auto-generated method stub

            String driver = "oracle.jdbc.driver.OracleDriver";
            String url = "jdbc:oracle:thin:@localhost:1521:xe";
            
            Connection con = null;   // 데이터베이스 접속
            Statement stmt = null;   // sql문 실행 시켜주는 역할
            ResultSet rs = null;     // select로 검색한 데이터를 관리하는 역할
            
            try {
               Class.forName(driver);// JDBC Driver Loading
               con = DriverManager.getConnection(url, "scott", "tiger");
               
               stmt = con.createStatement();
               
               String sql = "select * from customer";
               
               System.out.println("번호\t이름\t이메일\t\t전화번호");
               System.out.println("-------------------------------------------");
               
               rs = stmt.executeQuery(sql); // select SQL문 실행
               
               // boolean next()
               while(rs.next()) { // next(): 검색한 데이터를 1개씩 가져오는 역할
                  int no = rs.getInt("no");
                  String name = rs.getString("name");
                  String email = rs.getString("email");
                  String tel = rs.getString("tel");
                        
                  System.out.println(no+"\t"+name+"\t"+email+"\t"+tel);		
               }
            }catch(Exception e) {
               e.printStackTrace();
            }finally {
               try {
                  if(rs != null) rs.close();
                  if(stmt != null) stmt.close();
                  if(con != null) con.close();
               }catch(Exception e) {
                  e.printStackTrace();
               }
            }	
         }
      }
   ```

1. # Insert
   ```java
      public class JDBC_Insert {

         public static void main(String[] args) {
            // TODO Auto-generated method stub

            String driver = "oracle.jdbc.driver.OracleDriver";
            String url = "jdbc:oracle:thin:@localhost:1521:xe";
            
            Connection con = null;  // 데이터베이스 접속
            Statement stmt = null;  // sql문 실행 시켜주는 역할
            
            try {
               Class.forName(driver);
               con = DriverManager.getConnection(url, "scott", "tiger");
               
               stmt = con.createStatement();
               
               BufferedReader br = 
                  new BufferedReader(new InputStreamReader(System.in));
               
               System.out.print("회원번호 입력?");
               int no = Integer.parseInt(br.readLine());
               System.out.print("이름 입력?");
               String name = br.readLine();
               System.out.print("이메일 입력?");
               String email = br.readLine();
               System.out.print("전화번호 입력?");
               String tel = br.readLine();
               
               String sql = "insert into customer values ";
                     sql += " ("+ no +",'"+ name +"','"+ email +"','"+tel+"')";
                     
                  int result = stmt.executeUpdate(sql); // insert SQL문 실행
                  if(result == 1) {
                     System.out.println("회원가입 성공");
                  }else {
                     System.out.println("회원가입 실패");
                  }			
            }catch(Exception e) {
               e.printStackTrace();
            }finally {
               try {
                  if(stmt != null) stmt.close();
                  if(con != null) con.close();
               }catch(Exception e) {
                  e.printStackTrace();
               }
            }		
         }
      }
   ```

1. # Update
   ```java
      public class JDBC_Update {

         public static void main(String[] args) {
            // TODO Auto-generated method stub

            String driver = "oracle.jdbc.driver.OracleDriver";
            String url = "jdbc:oracle:thin:@localhost:1521:xe";
            
            Connection con = null;
            Statement stmt = null;
            
            try {
               Class.forName(driver);
               con = DriverManager.getConnection(url, "scott", "tiger");
               
               stmt = con.createStatement();
               
               BufferedReader br = 
                  new BufferedReader(new InputStreamReader(System.in));
               
               System.out.print("수정할 회원번호를 입력 하세요?");
               int no = Integer.parseInt(br.readLine());
               System.out.print("수정할 이름을 입력 하세요?");
               String name = br.readLine();
               System.out.print("수정할 이메일을 입력 하세요?");
               String email = br.readLine();
               System.out.print("수정할 전화번호를 입력 하세요?");
               String tel = br.readLine();
               
               String sql = "update customer set email='"+ email;			
                     sql += "',tel='"+ tel + "',name='"+name+"' where no="+ no;			
               
                  int result = stmt.executeUpdate(sql);//update SQL문 실행
                  if(result == 1) {
                     System.out.println("회원정보 수정 성공");
                  }else {
                     System.out.println("회원정보 수정 실패");
                  }
            }catch(Exception e) {
               e.printStackTrace();
            }finally {
               try {
                  if(stmt != null) stmt.close();
                  if(con != null) con.close();
               }catch(Exception e) {
                  e.printStackTrace();
               }
            }
         }
      }
   ```   

1. # Delete
   ```java
      public class JDBC_Delete {

         public static void main(String[] args) {
            // TODO Auto-generated method stub

            String driver = "oracle.jdbc.driver.OracleDriver";
            String url = "jdbc:oracle:thin:@localhost:1521:xe";
            
            Connection con = null;
            Statement stmt = null;
            
            try {
               Class.forName(driver);
               con = DriverManager.getConnection(url, "scott", "tiger");
               
               stmt = con.createStatement();
               
               BufferedReader br = 
                  new BufferedReader(new InputStreamReader(System.in));
               
               System.out.print("삭제할 회원번호를 입력 하세요?");
               int no = Integer.parseInt(br.readLine());
               
               String sql = "delete from customer where no=" + no;
               
               int result = stmt.executeUpdate(sql);
               if(result == 1) {
                  System.out.println("회원정보 삭제 성공");
               }else {
                  System.out.println("회원정보 삭제 실패");
               }
            }catch(Exception e) {
               e.printStackTrace();
            }finally {
               try {
                  if(stmt != null) stmt.close();
                  if(con != null) con.close();
               }catch(Exception e) {
                  e.printStackTrace();
               }
            }
         }
      }
   ```