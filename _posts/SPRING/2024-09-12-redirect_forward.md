---
layout: single
title: Redirect와 forward
categories: SPRING
tag: []
author_profile: false
---

1. # Redirect(재요청)
   1.클라이언트가 /ch2/write.jsp로 요청을 합니다.   

   2.응답 메시지
   ```
      HTTP/1.1 302
      Location:/ch2/login.jsp
      ContentlLanguage: ko-KR
      Content-Length: 0 Date:Sat, 13 Nov 2023 05:33:12 GMT
   ```   
   상태코드 300번대인 Redirect는 헤더만 있지 바디가 없습니다.   
   Location이 /ch2/login.jsp입니다.   

   3.사용자가 요청을 하는 것이 아니라 브라우저가 자동으로 Location을 읽어서 /ch2/login.jsp으로 요청을 합니다.   

   4.처음 클라언트가 요청한 method가 post든 get이든 상관없이 __Redirect는 get으로만 요청을 보냅니다.__   
   클라이언트가 /ch2/write.jsp로 요청을 했는데 서버가 ch2/login.jsp로 요청을 보낸 것입니다.   

   요약:   
   1./ch2/write.jsp로 요청   
   2.write.jsp에서 login.jsp로 가라고 응답   
   3.longin.jsp로 다시 요청   
   4.login.jsp에서 응답   
   => 요청도 2번, 응답도 2번   

1. # Forward(전달)
   1.클라언트가 /ch2/write.jsp로 요청   
   2.write.jsp에서 전달받은 데이터와 함께 login.jsp로 데이터를 전달   
   3.login.jsp가 처리 후 응답   
   => 요청 1번, 응답 1번   

   write.jsp에서 전달 시 request와 response를 같이 전달합니다.   
   login.jsp가 response를 통해 클라이언트에게 응답합니다.   

   forward예시   
   ```java
      @Controller
      public class DownloadEx {
         
         @RequestMapping("/download")
         public String downLoad(HttpServletRequest request, @RequestParam(required=false, defaultValue="")String type) {
         List<User> userList = getUserList();
         request.setAttribute("data", userList);
         
         if(type.equals("pdf")) {
            return "forward:/pdfView";
         }else if(type.equals("csv")) {
            return "forward:/csvView";
         }else {
            return "forward:/txtView";
         }
         }
         
         public List<User> getUserList(){
         return new List<User> list;
         }
      }
   ```

1. # Forward와 Redirect의 차이점
   __redirect__ 는 model이나 request객체를 <span style="color:red">직접 전달할 수 없습니다.</span>   
   __forward__ 는 model이나 request객체를 전달하여 <span style="color:red">다음 서블릿이나 JSP에서 사용할 수 있습니다.</span>   

   __Redirect (리다이렉트)__   
   클라이언트에게 새로운 URL을 전달하여 새로운 요청을 하도록 유도하는 방식입니다. 마치 브라우저 주소창에 <u>새로운 URL을 직접 입력 한 것과 같은 효과</u>를 냅니다. 따라서 클라이언트의 주소창에 URL이 변경됩니다.   
   요청과 응답 객체가 새로 생성되어 이전 서블릿에서 설정한 모델이나 attribute는 유지되지 않습니다.   
   두 번의 HTTP 요청이 발생합니다.   
   redirect는 본질적으로 새로운 요청을 시작하는 것이므로, 이전 요청의 데이터를 직접 전달할 방법이 없습니다. 만약 데이터를 전달해야 한다면, URL에 파라미터로 붙이거나, 세션에 저장하는 방법을 사용해야 합니다.   

   __Forward (포워드)__   
   서버 내부에서 다른 서블릿이나 JSP로 요청을 전달하는 방식입니다. 클라이언트는 이 과정을 인지하지 못합니다.   
   따라서 클라이언트의 주소창에 URL이 변경되지 않습니다.   
   요청과 응답 객체가 유지되어 이전 서블릿에서 설정한 모델이나 attribute를 다음 서블릿이나 JSP에서 사용할 수 있습니다.   
   한 번의 HTTP 요청으로 처리됩니다.   
   forward는 같은 요청 내에서 서블릿 간에 제어를 넘기는 것이므로, 모델이나 attribute를 공유하여 데이터를 전달할 수 있습니다.   
   
   =>
   Redirect: 클라이언트에게 완전히 새로운 요청을 시작하도록 하기 때문입니다. 이전 요청과의 연관성을 끊고 새로운 요청을 시작하는 것이 목적입니다.
   Forward: 서버 내부에서 처리되는 하나의 요청을 여러 서블릿이나 JSP에서 처리하기 위한 것이므로, 요청과 응답 객체를 공유하여 데이터를 전달할 수 있습니다.   

1. # Forward와 Redirect의 Method방식
   __Redirect (리다이렉트)__   
   주로 GET 방식: redirect는 기본적으로 새로운 요청을 시작하기 때문에 GET 방식을 사용하는 것이 일반적입니다.   
   POST 데이터 유실: POST 방식으로 전송된 데이터는 redirect 시 유실될 수 있습니다.   
   
   -POST 데이터 전달 방법-   
   URL 파라미터: RedirectAttributes를 이용하여 URL 파라미터에 데이터를 추가할 수 있습니다. 하지만 민감한 정보를 노출할 수 있으므로 주의해야 합니다.   
   세션: HttpSession을 이용하여 세션에 데이터를 저장하고, 다음 요청에서 해당 데이터를 가져올 수 있습니다.   
   쿠키: 쿠키를 이용하여 데이터를 저장할 수 있지만, 보안 문제가 발생할 수 있으므로 신중하게 사용해야 합니다.   

   __Forward (포워드)__   
   POST/GET 모두 지원: forward는 서버 내부에서 처리되는 것이므로 POST/GET 방식에 상관없이 데이터를 전달할 수 있습니다.   

   -데이터 전달 방법-   
   Model: Model 인터페이스를 이용하여 데이터를 추가하고, 다음 서블릿이나 JSP에서 해당 데이터를 사용할 수 있습니다.   
   Request 객체: HttpServletRequest 객체를 이용하여 요청 파라미터를 직접 가져올 수 있습니다.   

   각 방식의 특징과 사용 시 주의사항   
   
   |  방식  |POST/GET 지원|데이터 전달 방법|  주의사항  | 
   |:------:|:-----------:|:-------------:|:---------:|
   | Redirect | 주로 GET방식 |	URL 파라미터, 세션, 쿠키 |	POST 데이터 유실 가능, 보안 문제 발생 가능 |
   | Forward  |	POST/GET | Model, Request 객체 | 서버 내부 처리, 보안에 취약할 수 있음 |

