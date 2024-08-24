---
layout: single
title: (MVC)관심사의 분리
categories: SPRING
tag: []
author_profile: false
---

1. # 관심사란?
   클라이언트로부터 요청을 받았을 때 이를 처리하는 과정은 "클라이언트의 데이터입력 → 작업 처리 → 출력" 3부분으로 나눠 볼 수 있습니다. 입력, 처리, 출력 3부분이 전부 개발자들이 __관심을 가지고 처리__ 를해야할 작업들입니다. 관심사란 "개발자들이 해야할 작업" 정도로 이해할 수 있습니다.   

1. # main에 관심사

   ```java   
      public class YoilTeller {
         @RequestMapping("/getYoil")
         public void main(HttpServletRequest request, HttpServletResponse response) throws IOException {

            // 1. 입력  <-------------------------------------------------------- 하나의 관심사
            String year = request.getParameter("year");
            String month = request.getParameter("month");
            String day = request.getParameter("day");

            int yyyy = Integer.parseInt(year);
            int mm = Integer.parseInt(month);
            int dd = Integer.parseInt(day);

            // 2. 처리  <-------------------------------------------------------- 하나의 관심사
            Calendar cal = Calendar.getInstance();
            cal.set(yyyy, mm - 1, dd);
            int dayOfWeek = cal.get(Calendar.DAY_OF_WEEK);
            char yoil = " 일월화수목금토".charAt(dayOfWeek);

            // 3. 출력  <-------------------------------------------------------- 하나의 관심사
            response.setContentType("text/html");  
            response.setCharacterEncoding("utf-8");  
            PrintWriter out = response.getWriter();  
            out.println("<html>");
            out.println("<head>");
            out.println("</head>");
            out.println("<body>");
            out.println(year + "년 " + month + "월 " + day + "일은 ");
            out.println(yoil + "요일입니다.");
            out.println("</body>");
            out.println("</html>");
            out.close();
         }
   ```   
   main 클래스에는 다음과 같이 입력, 처리, 출력 3개의 관심사가 있습니다. 하나의 main 함수에 3가지 관심사가 있기 때문에 객체지향 5대 원칙 SOLID 중 S인 단일 책임 원칙에 위배됩니다. 이들 관심사를 분해하여 "하나의 메서드는 하나의 책임"만 관리하는 원칙을 적용해 보겠습니다.   

1. # 입력 부분 분리
   ```java
      public class YoilTeller {
            @RequestMapping("/getYoil")
            public void main(int year, int month, int day, HttpServletResponse response) throws IOException {
               
            // 입력 부분 생략 가능.

            // 2. 처리
            Calendar cal = Calendar.getInstrance();
            cal.set(year, month-1, day);
            ...
   ```   
   public void main(int year, int month, int day, HttpServletResponse response)  
   변수 year, month, day를 getParameter로 받아서 Interger.parseInt 과정을 해준 후 year, month, day 변수를 가져올 수 있었는데 main메소드의 매개변수에서 바로 int형으로 변수 year, month, day 값을 가져왔습니다.   

1. # Model객체의 필요성
   처리와 출력 부분이 하나의 main 메소드에 있을 땐 바로 접근해서 변수 year, month, day를 사용할 수 있었지만, 따로 분리되면 처리 부분, 출력 부분 사이에 변수를 주고 받을 무엇인가가 필요합니다. 이 작업을 Model이라는 객체가 하게 됩니다. 변수들을 Model 객체에 입력 후 이 객체를 서로 주고 받음으로써 변수 값을 가져올 수 있습니다.   

   처리 부분은 Controller가 관리   

   변수값 저장 Model   

   출력 부분은 View가 관리   

   이렇게 구성되어 있는 것을 MVC 패턴이라고 읽습니다.   

1. # Spring에서 MVC

   __입력부분__ Dispatcher Servlet (Model) ↔ (Model) __처리부분__ Controller   
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↑↓(Model)   
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __출력부분__ View   
   <span style="color:red;font-weight:bold;font-size:14px">*데이터 전송은 Model 객체로 전송</span>

   입력을 받으면 Dispatcher Servlet 부분에서 입력처리 작업에 필요한 변수를 Model에 담아서 Controller에 넘기고, Controller에서 작업을 처리한 결과를 Model에 담아서 다시 Dispatcher Servlet에게 넘기면, Dispatcher Servlet이 받은 결과를 View에게 넘기게 되고, View가 요청이 이루어진 곳은 데이터를 전송하는 방식으로 MVC패턴이 동작하게 됩니다.   

   ```java

      //Controler 부분
      public class YoilTellerMVC {
         @RequestMapping("/getYoilMVC") 
         public String main(int year, int month, int day, Model model) {   //1.입력 부분과 Model 생성
            
            // 2. 처리
            char yoil = getYoil(year, month, day); //getYoil에서 작업을 처리 후 결과를 yoil에 받음

            // 3. Model에 작업 결과 저장
            model.addAttribute("year", year);
            model.addAttribute("month", month);
            model.addAttribute("day", day);
            model.addAttribute("yoil", yoil);
            
            // 4. 작업 결과를 보여줄 View의 이름을 반환
            return "yoil"; // /WEB-INF/views/yoil.jsp => DispatcherServelt으로 넘겨준다
         }
         
      // 중간에 DispatherServlet이 있고, return "yoil" 값을 보고 해당 View로 넘긴다

      //View 부분 - yoil.jsp
      <%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
      <html>
      <head>
         <title>YoilTellerMVC</title>
      </head>
      <body>
         <h1>${year}년 ${month}월 ${yoil}요일 입니다</h1>
      </body>
      </html>
   ```