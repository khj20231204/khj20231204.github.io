---
layout: single
title: MVC2
categories: SPRING(Lesson)
tag: []
author_profile: false
---

1. # 주요 기능
   1.Connection Pool   
   2.request, session 객체 공유 설정   
   3.Controller클래스 : Java Servlet   
   4.Model = Service + DAO   
      Service, DTO, DAO 클래스   
   5.View(화면 인터페이스) : EL, JSTL사용   

1. # 프로그램 주요 파일
   Controller클래스 - MemberController.java   

   DTO클래스 : model - MemberDTO.java(DTO크래스)   
   DAO클래스 : dao - MemberDAO.java(DAO클래스)   

   Action인터페이스 : service - Action.java   
   
   ActionForward클래스 : service - ActionForwad.java   

   Service클래스 : service =>   
   MemberInert.java(회원가입)    
   IdCheck.java(ID중복검사)   
   Login.java(로그인)   
   Logout.java(로그아웃)   
   UpdateMember.java(정보수정폼)   
   Update.java(정보수정)   
   DeleteMember.java(회원탈퇴폼)   
   Delete.java(회원탈퇴)   

1. # 작성 순서

   controller -> service -> dao -> service -> controller -> view

   1)DB파일을 가져와서 DTO만들기   
   2)DAO만들기   
   3)Servlet - Controller만들기
   :memberForm.jsp -> Controller   
   =>memberForm.jsp의 form action으로 Controller의 .do로 전송   
   4)Service - 부모 인터페이스(Action) 만들기   
   5)Service - ActionForward 클래스 만들기   
   6)Service - MemberInert 클래스 만들기

1. # DAO만들기
   dbcp방식 - Connection Pool   

   ```java
      public class MemberDAO {
         private static MemberDAO instance = new MemberDAO(); 
               
         public static MemberDAO getInstance() {
            return instance;
         }
         
         //컨넥션풀에서 컨넨ㄱ션을 구해오는 메소드
         private Connection getConnection() throws Exception {
            Context init = new InitialContext();
            DataSource ds = (DataSource) init.lookup("java:comp/env/jdbc/orcl");
            return ds.getConnection();
         }
         
         //회원가입
         public int insert(MemberDTO member) {
            int result = 0;
            return result;
         }
      }
   ```

1. # Controller - servlet
   File -> New -> Servlet으로 생성   

   1)톰캣 버전 9점 대 - 어노테이션으로 추가   
   ```java
      /* @WebServlet("/MemberController") */
      @WebServlet("*.do") //do확장자로 요청하는 모든 요청을 받는다는 의미
      public class MemberController extends HttpServlet {
         private static final long serialVersionUID = 1L;

         protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            response.getWriter().append("Served at: ").append(request.getContextPath());
         }

         protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            doGet(request, response);
         }
      }
   ```

   2)톰캣 버전 10점 대 - WEB-INF/web.xml 파일에 servlet이 자동 맵핑됨   
   ```xml
      <servlet>
         <description></description>
         <display-name>MemberController</display-name>
         <servlet-name>MemberController</servlet-name>
         <servlet-class>Controller.MemberController</servlet-class>
      </servlet>
      <servlet-mapping>
         <servlet-name>MemberController</servlet-name>
         <url-pattern>/MemberController</url-pattern>
      </servlet-mapping>
   ```

1. # 실행순서
   로그인 session 이 있다 - main페이지
   sesstio이 이 없다 - 로그인

   memberForm.jsp -> MemberInsert.do(controller) -> 

   main.jsp -> UpdateMember.do(controller) : controller에서

   