---
layout: single
title: 태그와 선언
categories: JSP(Lesson)
tag: []
author_profile: false
---

1. # jsp
   
   __5대 Tag__   

   1. ## 선언 태그   
      ```jsp
         <%! ... %>
      ```   
      클래스,메소드를 선언하는 구역입니다. 하지만 JSP에서는 클래스나 메소드를 잘 선언하지 않기 때문에 선언 태그 사용 빈도는 낮습니다.   

      예제)   
      ```jsp
         <%!
            int a = 30; //선언 태그 안에서 변수는 사용 가능
            public int add(int a, int b){
               return a+b;
            }
         %>
      ```
   
   1. ## 스크립트릿   
      ```jsp
         <% ... %>
      ```   
      일반적인 자바 표현을 나타냅니다.   

      ```jsp
         <%
            //선언태그의 add함수 결과 받기
            int result = add(4,5);

            //기본 자료형 변수
            int i = 30;
            double d = 3.14;
            char c1 = 'A';
            char c2 = '자';
            boolean b1 = true;
            boolean b2 = false;
            
            //참조형 변수
            //1.클래스
            String str1 = "JSP";
            String str2 = new String("JSP");
            
            String[] str = {"자바","jsp","오라클","웹 표준"};
            
            for(String s : str){
               out.println(s + "\t");
            }
            out.println("<br>");
            
            for(String s : str){
               %>
                  <%= s %><br>
               <%
            }
            
            //2.인터페이스
            List list = new ArrayList();    // 업캐스팅
            list.add(50);
            list.add(42.195);
            list.add('A');
            list.add(true);
            list.add("JSP");
            
            for(int j=0; j<list.size(); j++){
               out.println(list.get(j)+"\t");
            }    
            
            out.print("<br>");
         %>
      ```   
   
   1. ## 표현식 태그   
      ```jsp
         <%= ... %>
      ```   
      브라우저에 값 출력, 변수값 출력   
      ```jsp
         add : <%= result %>

         출력 : <%= "출력 성공" %><br>
         연산 결과 : <%= 1+2+3+4+5+6 %><br>
         i : <%= i %><br>
         d : <%= d %><br>
         c1 : <%= c1 %><br>
         c2 : <%= c2 %><br>
         b1 : <%= b1 %><br>
         b2 : <%= b2 %><br>
         str1 : <%= str1 %><br>
         str2 : <%= str2 %><br>
      ```

   1. ## 지시어 태그   
      1)페이지 태그   
      ```jsp
         <!-- 선언 방식 -->
         <%@ page ... %>

         <!-- 예제 -->
         <%@ page contentType="text/html; charset=UTF-8" %>
         <%@ page import="java.util.Date" %>
         <%@ page errorPage = "/error/viewErrorMessage.jsp" %>
         <%@ page isErrorPage = "true" %>
      ```

      2)포함 태그   
      ```jsp
         <%@ include ... %>
      ```   

      3)사용자 정의 태그   
      ```jsp
         <%@ taglib ... %>
      ```

      4)액션 태그   
      ```jsp
         <jsp:usebean ... >, <jsp:setProperty ... >
         <jsp:forward ... >, <jsp:include ... >
      ```

1. # import 속성 활용

   ```jsp
      <%@ page import="java.util.List" %>      
      <%@ page import="java.util.*" %>   
      <%@ page import="com.example.MyClass" %>
     
      <body>
         <%
            List<String> list = new ArrayList<>();

            MyClass myClass = new MyClass();
            String message = myClass.getMessage();
            out.println(message);
         %>
      </body>
   ```   

1. # 날짜 데이터가져오기   
   ```jsp
      <%@ page import="java.util.*"  %>

      <%
         //날짜, 시간 관련 클래스

         //1. Date클래스
         //한번만 사용하는 경우 이렇게 해도 된다
         //java.util.Date d = new java.util.Date();

         //날짜 가져오기
         Date d = new Date();
         //날짜 형식 지정, Date에는 형식 지정하는 메서드가 없다
         SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss EEE요일");
         String s = sdf.format(d);
         
         //2.TimeStamp클래스
         Timestamp ts = new Timestamp(System.currentTimeMillis());
         String s2 = sdf.format(ts);
         
         //3.Calendar클래스
         Calendar calendar = Calendar.getInstance();
         
         int year = calendar.get(Calendar.YEAR);	//연도
         int month = calendar.get(Calendar.MONTH)+1; //월(0~11)
         int day = calendar.get(Calendar.DATE); //일
         
         int hour1 = calendar.get(Calendar.HOUR);
         int hour2 = calendar.get(Calendar.HOUR_OF_DAY);
         
         String h = "";
         if(calendar.get(Calendar.AM_PM) == 0){
            h = "오전";		//AM_PM : 0(오전)
         }else{
            h = "오후";		//AM_PM : 1(오후)
         }
         
         int minute = calendar.get(Calendar.MINUTE);
         int second = calendar.get(Calendar.SECOND);
         
         String[] yoil = {"일요일","월요일","화요일","수요일","목요일","금요일","토요일"};
         String yoil_print = yoil[calendar.get(Calendar.DAY_OF_WEEK)];
      %>

      현재시간Date : <%= d %><br>
      현재시간Date-simpleFormat : <%= s %><br>
      현재시간Timestamp : <%= ts %><br>
      현재시간Timestamp-simpleFormat : <%= s2 %><br>

      <!-- 12시간제 -->
      <%= year %> - <%= month %> - <%= day %> <%= h %> <%= hour1 %>시(<%= hour2 %>시) : <%= minute %> : <%= second %> <%= yoil_print %>
   ```
