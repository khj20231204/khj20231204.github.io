---
layout: single
title: 서블릿과 JSP
categories: SPRING
tag: []
author_profile: false
---

1. # 서블릿과 컨트롤러
    서블릿의 발전된 단계가 컨트롤러입니다

    ```java
        @WebServlet("/hello")
        public class HelloServlet extends HttpServlet {

            @Override
            public void init() throws ServletException {
                //서블릿 초기화 - 서블릿이 생성또는 리로딩될 때, 단 한번만 수행됨
                System.out.println("[HelloServlet] init()");
            }
                @Override //호출될 때마다 반복적으로 수행됨
            protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
                //1.입력
                //2.처리
                //3.출력
                System.out.println("[HelloServlet] servoce()");
            }

            @Override
            public void destroy() {
                //뒷정리 작업 - 서블릿이 제거(unload)될 때, 단 한번만 수행됨.
                System.out.println("[HelloServlet] destroy()");
            }
    ```   
    요청이 들어오면 서블릿 컨테이너가 서블릿 인스턴스의 존재를 파악하게 됩니다. 만들어둔 서블릿 인스턴스가 없다면 init()메서드를 한번 호출하게 되고 이후 service()메서드로 작업을 합니다. 그 결과를 return하게 되고, 이후 작업이 들어오면 service()만 호출하게 됩니다. 서버가 종료될 때나 reload될 때 destory()메서드가 한번 실행됩니다.   
    간단히, 최조 init()메소드를 한번 실행하게 되고 이후 서버가 종료될 때나 reload될 때 destory()메서드가 한번 실행됩니다. 실제 입력,처리,출력되는 모든 작업은 service메소드에서 실행이되는데 메서드 호출은 서블릿 컨테이너가 처리를 하게됩니다.   
    서블릿은 싱글톤으로 실행되며 클라이언트로 작업이 입력될 때마다 service가 실행됩니다.   

    서블릿과 컨테이너의 비교
    ```java
        //서블릿
        @WebServlet("/rollDice2")
        public class TwoDiceServlet extends HttpServlet {
            int getRandomInt(int range) {
            return new Random().nextInt(range)+1;
            }

            public void service(HttpServletRequest request, HttpServletResponse response) throws IOException {
                int idx1 = getRandomInt(6);
                int idx2 = getRandomInt(6);

                response.setContentType("text/html");
                response.setCharacterEncoding("utf-8");
                PrintWriter out = response.getWriter();
                out.println("<html>");
                out.println("<head>");
                out.println("</head>");
                out.println("<body>");
                out.println("<img src='resources/img/dice"+idx1+".jpg'>");
                out.println("<img src='resources/img/dice"+idx2+".jpg'>");
                out.println("</body>");
                out.println("</html>");
                out.close();	    
            }
        }

        //컨테이너
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
    @WebServlet은 @Controller와 @RequestMapping 두 개의 기능을 합쳐놓은 것입니다. WebServlet은 클래스에 선언을 하기 때문에 다른 경로의 주소를 새로 만들 때마다 클래스를 새로 생성해야합니다. 그러한 단점을 개선하기 위해 메서드 단위로 주소를 맵핑시키는 ReqeustMapping이 도입되었습니다.   
    서블릿은 response를 HttpServlet으로 상속받아서 service를 오버로딩하는 방식으로 사용하는데 컨트롤러는 main(HttpServletResponse response)처럼 매개변수로 받아서 사용하게 됩니다. 자바는 단일 상속을 받는다는 점에서 서블릿을 개선한 모습을 컨트롤러에서 볼 수 있습니다.   

1. # JSP의 호출
    JSP는 HTML안에 자바코드가 있는 것입니다. 
    twoDice.jsp요청이 들어온다.   

    확장자가 jsp인 파일이 들어오면 JspServlet이 모두(*.jsp) 받아서 서블릿 인스턴스의 존재를 파악한다.   

    twoDice.jsp로 만든 서블릿이 없는 경우 twoDice.jsp를 서브릿 소스파일로 변환한다.   
    ex)twoDice.jsp => twoDice.java   

    서블릿 파일로 변환 후 컴파일해서 class파일을 만든다.   
    ex)twoDice.java => twoDice.class   

    twoDice.java를 이용해서 객체를 생성한다. 이때 jspInit() 메소드 호출   

    서블릿 인스턴스에서 요청처리 jspService()   

    init()는 초기화, Service()는 요청처리   

    : 최초 호출 시에만 변환 후 객체 생성까지 지연시간이 있고, 이후부터는 바로 객체로 간다

1. # JSP의 기본 객체
    ```jsp
        <%@ page contentType="text/html;charset=utf-8"%>
        <%@ page import="java.util.Calendar" %>
        <%
            String year  = request.getParameter("year");
        %>
    ```   
    request.getParameter는 객체 생성없이 바로 사용된다. JSP자체에서 기본 객체를 제공하기 때문이다.  