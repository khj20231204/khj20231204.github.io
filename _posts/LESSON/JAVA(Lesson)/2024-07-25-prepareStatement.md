---
layout: single
title: 07_25.PrepareStatement문으로 작성
categories: JAVA(Lesson)
tag: []
author_profile: false
---

1. # Select
   ```java
      public class JDBC_Select01 {

         public static void main(String[] args) {
            // TODO Auto-generated method stub

            String driver = "oracle.jdbc.driver.OracleDriver";
            String url = "jdbc:oracle:thin:@localhost:1521:xe";
            
            Connection con = null;
            PreparedStatement pstmt = null;
            ResultSet rs01 = null;
            ResultSet rs02 = null;
            
            int cnt = 0; // 회원수
            
            try {
               Class.forName(driver);
               con = DriverManager.getConnection(url, "scott", "tiger");
               
               String sql = "select count(*) from customer";
               
               pstmt = con.prepareStatement(sql);
               rs01 = pstmt.executeQuery(); // select SQL문 실행
               if(rs01.next()) {
                  cnt = rs01.getInt(1);
      //				cnt = rs01.getInt("count(*)");
               }
               System.out.println("총 회원수:"+ cnt);
               
               
               sql = "select * from customer";
               pstmt = con.prepareStatement(sql);
               rs02 = pstmt.executeQuery(); // select SQL문 실행
               
               System.out.println("번호\t이름\t이메일\t\t전화번호");
               System.out.println("-------------------------------------");
               
               while(rs02.next()) {
                  int no = rs02.getInt("no");
                  String name = rs02.getString("name");
                  String email = rs02.getString("email");
                  String tel = rs02.getString("tel");
                  
                  System.out.println(no+"\t"+name+"\t"+email+"\t"+tel);
               }			
            }catch(Exception e) {
               e.printStackTrace();
            }finally {
               try {
                  if(rs01 != null) rs01.close();
                  if(rs02 != null) rs02.close();
                  if(pstmt != null) pstmt.close();
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
      public class JDBC_Insert01 {

         public static void main(String[] args) {
            // TODO Auto-generated method stub

            String driver = "oracle.jdbc.driver.OracleDriver";
            String url = "jdbc:oracle:thin:@localhost:1521:xe";
            
            Connection con = null;
            PreparedStatement pstmt = null;
            
            try {
               Class.forName(driver);
               con = DriverManager.getConnection(url, "scott", "tiger");
               
               BufferedReader br = 
                  new BufferedReader(new InputStreamReader(System.in));
               
               System.out.print("회원번호 입력?");
               int no = Integer.parseInt(br.readLine());
               System.out.print("회원이름 입력?");
               String name = br.readLine();
               System.out.print("이메일주소를 입력?");
               String email = br.readLine();
               System.out.print("전화번호를 입력?");
               String tel = br.readLine();
               
               String sql = "insert into customer values(?,?,?,?)";
               
               pstmt = con.prepareStatement(sql);
               pstmt.setInt(1, no);
               pstmt.setString(2, name);
               pstmt.setString(3, email);
               pstmt.setString(4, tel);
               
               int result = pstmt.executeUpdate(); // insert SQL문 실행
               if(result == 1) {
                  System.out.println("회원가입 성공");
               }else {
                  System.out.println("회원가입 실패");
               }
            }catch(Exception e) {
               e.printStackTrace();
            }finally {
               try {
                  if(pstmt != null) pstmt.close();
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
      public class JDBC_Update01 {

         public static void main(String[] args) {
            // TODO Auto-generated method stub
            
            String driver = "oracle.jdbc.driver.OracleDriver";
            String url = "jdbc:oracle:thin:@localhost:1521:xe";
            
            Connection con = null;
            PreparedStatement pstmt = null;
            
            try {
               Class.forName(driver);
               con = DriverManager.getConnection(url, "scott", "tiger");
               
               BufferedReader br = 
                  new BufferedReader(new InputStreamReader(System.in));
               
               System.out.print("수정할 회원번호를 입력?");
               int no = Integer.parseInt(br.readLine());
               System.out.print("수정할 회원이름을 입력?");
               String name = br.readLine();
               System.out.print("수정할 이메일주소를 입력?");
               String email = br.readLine();
               System.out.print("수정할 전화번호를 입력?");
               String tel = br.readLine();
               
               String sql = "update customer set name=?,email=?,";
                     sql += "tel=? where no=?";
                     
               pstmt = con.prepareStatement(sql);
               pstmt.setString(1, name);
               pstmt.setString(2, email);
               pstmt.setString(3, tel);
               pstmt.setInt(4, no);
               
               int result = pstmt.executeUpdate(); // update SQL문 실행
               if(result == 1) {
                  System.out.println("회원정보 수정 성공");
               }else {
                  System.out.println("회원정보 수정 실패");
               }
            }catch(Exception e) {
               e.printStackTrace();
            }finally {
               try {
                  if(pstmt != null) pstmt.close();
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
      public class JDBC_Delete01 {

         public static void main(String[] args) {
            // TODO Auto-generated method stub
            
            String driver = "oracle.jdbc.driver.OracleDriver";
            String url = "jdbc:oracle:thin:@localhost:1521:xe";
            
            Connection con = null;
            PreparedStatement pstmt = null;
            
            try {
               Class.forName(driver);
               con = DriverManager.getConnection(url, "scott", "tiger");
               
               BufferedReader br = 
                  new BufferedReader(new InputStreamReader(System.in));
               
               System.out.print("삭제할 회원번호를 입력 하세요?");
               int no = Integer.parseInt(br.readLine());
               
               String sql = "delete from customer where no= ?";
               
               pstmt = con.prepareStatement(sql);
               pstmt.setInt(1, no);
               
               int result = pstmt.executeUpdate();// delete SQL문 실행			
               if(result == 1) {
                  System.out.println("회원정보 삭제 성공");
               }else {
                  System.out.println("회원정보 삭제 실패");
               }
            }catch(Exception e) {
               e.printStackTrace();
            }finally {
               try {
                  if(pstmt != null) pstmt.close();
                  if(con != null) con.close();
               }catch(Exception e) {
                  e.printStackTrace();
               }
            }
         }
      }
   ```