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

  사용자가 요청을 하는 것이 아니라 브라우저가 자동으로 Location을 읽어서 /ch2/login.jsp으로 요청을 합니다.   

  처음 클라언트가 요청한 method가 post든 get이든 상관없이 __Redirect는 get으로만 요청을 보냅니다.__   
  클라이언트가 /ch2/wirte.jsp로 요청을 했는데 서버가 ch2/login.jsp로 요청을 보낸 것입니다.   

  1./ch2/write.jsp로 요청   
  2.write.jsp에서 login.jsp로 가라고 응답   
  3.longin.jsp로 다시 요청   
  4.login.jsp에서 응답   
   => 요청도 2번, 응답도 2번   

1. # Forward(전달)
   1.클라언트가 /ch2/write.jsp로 요청   
   2.write.jsp에서 전달받은 데이터와 함께 login.jsp로 데이터를 전달   
   3.login.jsp가 처리 후 응답   

   write.jsp에서 전달 시 