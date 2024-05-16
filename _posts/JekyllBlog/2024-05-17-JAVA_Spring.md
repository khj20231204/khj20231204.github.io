---
layout: single
title: JAVA Spring
categories: JekyllBlog
tag: []
---

1. # Spring에서 Bean
   Spring에서 Bean은 스프링 IoC 컨테이너가 생성하고 관리하는 Java 객체를 뜻한다.
   일반 Java 객체와 다른 점은 없고, 단지 스프링 IoC 컨테이너에서 관리하는 객체이다. 스프링에서 생성되고, 라이프 사이클을 수행하고, 의존성 주입이 일어나는 개체들을 말한다.
 
1. # @Component
   개발자가 생성한 Class를 Spring의 Bean으로 등록할 때 사용하는 어노테이션   

1. # @ComponentScan
   Spring Framework는 @Component, streotype(@Service, @Repository, @Controller:@component를 포함하고 있다), @Configuration 어노테이션이 부여된 클래스들을 자동으로 검색하여 Bean으로 등록해주는 역할을 하는 어노테이션   

1. # @Bean
   @Bean과 @Component 어노테이션은 둘 다 Spring IoC Container에 Bean을 등록하도록하는 메타데이터를 기입하는 어노테이션 
   @Bean : 개발자가 제어 불가능한 외부 라이브러리 등을 Bean으로 만들려고할 때 사용   
   @Component : 개발자가 직접 작성한 클래스를 Bean으로 등록할 때 사용   

1. # @Controller
   Spring MVC패턴에서 컨트롤러 역할을 하는 클래스를 표시할 때 사용

1. # @RequestHeader
   웹 header에 바운딩된 데이터를 가져온다. Body가 없는 get이나 Delete의 데이터를 가져올 때 사용

1. # @RequestMapping
   특정 uri로 요청을 보내면 controller에서 어떤 방식으로 처리할지 정의한다. 이때 들어온 요청을 특정 메서드와 맵핑하기 위해서 사용
   ```java
      @RequestMapping(value = "/hello", method = RequestMethod.GET)
      public String helloGet(...) { //hello uri로 get방식으 들어오면 호출
         ...
      }

      @RequestMapping(value = "/hello", method = RequestMethod.POST)
      public String helloPost(...) { //hello uri로 post방식으로 들어오면 호출
         ...
      }
    ```

1. # @RequestParam
   url에 전달되는 파라미터를 메소드의 인자와 매칭시켜, 파라미터를 받아서 처리   

1. # @RequestBody 
   웹 body에 바운딩된 데이터를 가져온다. Body가 있는 post나 Put의 데이터를 가져올 때 사용   

1. # @ResponseBody
   클라이언트 → 서버 : 요청(request), 클라이언트가 서버에 데이터를 요청   
   클라이언트 ← 서버 : 응답(response), 서버가 클라이언트의 요청에 대해 응답   

   클라이언트에서 서버로 필요한 데이터를 요청하기 위해 JSON 데이터를 요청 본문에 담아서 서버로 보내면, 서버에서는 @RequestBody 어노테이션을 사용하여 HTTP 요청 본문에 담긴 값들을 자바객체로 변환시켜, 객체에 저장한다.    
   서버에서 클라이언트로 응답 데이터를 전송하기 위해 @ResponseBody 어노테이션을 사용하여 자바 객체를 HTTP 응답 본문의 객체로 변환하여 클라이언트로 전송한다. 

1. # @ModelAttribute
   -메소드에 선언한 경우   
   해당 메소드가 반환하는 객체를 Model을 통해 뷰에 전달.   
   -파라미터에 선언한 경우   
   

1. # Model 객체
   Controller에서 생성된 데이터를 담아 view로 전달할 때 사용하는 객체.   
   servlet의 request.setAttribute()와 비슷한 역할을 함

1. # 스프링 컨텍스트
   스프링이 관리하는 빈들이 담겨있는 컨테이너   
   -ROOT-CONTEXT(공통 부분)   
   모든 서블릿이 공유할 수 있는 Bean들이 모인 공간. DB와 관련된 Repository, Service 등이 있음.   
   -SERVLET-CONTEXT(개별 부분)   
   서블릿 각자의 Bean들이 모인 공간. 웹, 앱 마다 한 개씩 존재하므로 웹 앱 그 자체를 의미하기도 함. 이 Context 내에서의 Bean들은 서로 공유될 수 없음. MVC의 Controller가 이에 해당