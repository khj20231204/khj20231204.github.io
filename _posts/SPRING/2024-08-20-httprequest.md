---
layout: single
title: HttpServletRequest와 yoilTeller(인코딩), dice(이미지 경로)
categories: SPRING
tag: []
author_profile: false
---

1. # HttpServletRequest

   ```java
      @Controller
      public class RequestInfo{
         @RequestMapping("/requestInfo")
         public void main(HttpServeltRequest request){
            System.out.println(request.getMethod());
		      System.out.println(request.getLocalAddr());
         }
      }
   ```   

   주소창에 `http://111.222.333.444:8080/ch2/requestInfo?addinfo='aaa'` 다음과 같은 주소를 치게되면 톰캣이 HttpServletRequest의 객체를 만들어서 주소에 있는 정보를 객체에 집어넣습니다. 그 객체를 request로 받아서 request.getMethod(), request.getLocalAddr() 등의 메소드와 함께 사용합니다. 

1. # URL 분석

   ```
      http://111.222.333.444:8080/ch2/requestInfo?year=2021&month=10&day=1
   ```   
   http - getScheme()   
   111.222.333.444 - getServerName()   
   8080 - getServerPort()   
   ch2 - getConextPath()   
   requestInfo - getServletPath()   
   year=2021&month=10&day=1 - getQeuryString()   

   ch2/requestInfo - getRequestURI()   

   http://111.222.333.444:8080/ch2/requestInfo - getRequestURL()   

1. # getQueryString
   ```
      ?year=2021&month=10&day=1   
   ```   
   name : year , value : 2021   
   name : month , value : 10   
   name : day , value : 1   

   QueryString에 name을 변수로 받아와서 value를 구합니다.   
   ```java
      String {value} = request.getParamter({name});

      String year = request.getParameter("year");
      String month = request.getParameter("month");
      String day = request.getParamter("day");
   ```   
   year, month, day는 숫자지만 전부 문자열 취급합니다. url자체가 문자열이기 때문입니다.   

1. # getParameter()
   만약 year, month, day와 같은 name만 가져오고 싶다면 getParamterNames()를 이용합니다.   
   ```java
      Enumeration enum = request.getParamerNames();
   ```   
   Enumeration - old버전, Iterator - new버전으로 사용법은 서로 비슷합니다.   

1. # getParameterMap()
   QueryString의 name과 value를 map형식으로 가져오려면 getParameterMap()을 이용합니다.   
   ```java
      Map paramMap = request.getParameterMap();
   ```   

1. # getParameterValues()
   name의 이름이 같은 경우 getParameterValues()를 이용해서 받아옵니다.   
   
   ```java
      ?year=2022&year=2023&year=2024

      String[] yearArr = request.getParameterValues("year");
   ```   
   Values뒤에 's'가 붙습니다. name이 year인 값들을 __배열__ 로 받습니다.   
   2022, 2023, 2024 형태는 숫자지만 url자체가 문자기 때문에 String으로 받았습니다.   

1. # yoilTeller
   ```java

      @Controller //프로그램 등록
      public class YoilTeller {
         @RequestMapping("/getYoil") // http://localhost:8080/ch2/getYoil?year=2021&month=10&day=1
         public void main(HttpServletRequest request, HttpServletResponse response) throws IOException {
            //request 응답을 받는다. response 응답을 보낸다

            //입력
            String year = request.getParameter("year");
            String month = request.getParameter("month");
            String day = request.getParameter("day");

            int yyyy = Integer.parseInt(year);
            int mm = Integer.parseInt(month);
            int dd = Integer.parseInt(day);

            // 2. 처리
            Calendar cal = Calendar.getInstance();
            cal.set(yyyy, mm - 1, dd);

            int dayOfWeek = cal.get(Calendar.DAY_OF_WEEK);
            char yoil = " 일월화수목금토".charAt(dayOfWeek);

            // 3. 출력
            response.setContentType("text/html");    // 응답의 형식을 html로 지정
            response.setCharacterEncoding("utf-8");  // 응답의 인코딩을 utf-8로 지정, 인코딩이 없으면 한글이 깨짐
            PrintWriter out = response.getWriter();  // response를 통해 브라우저로의 출력 스트림(out)을 얻는다.
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
      }
   ```   

1. # dice
   ```java
      @Controller
      public class TwoDice {
         
         @RequestMapping("/rollDice")
         public void main(HttpServletResponse response) throws Exception {
            
            int n = (int)((Math.random()*6)+1);
            
            response.setContentType("text/html");
            response.setCharacterEncoding("utf-8");
            PrintWriter out = response.getWriter();
            out.println("<html>");
            out.println("<head>");
            out.println("</head>");
            out.println("<body>");
            out.println("<img src='resources/img/dice"+n+".jpg'>"); 
            out.println("</body>");
            out.println("</html>");
         }
      }
   ```   
   이미지 경로는 
   img/dice1.jpg (x)   
   /img/dice1.jpg (x)   
   /resources/img/dice1.jpg (x)   
   
   __resources/img/dice.jpg (o)__   
