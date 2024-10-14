---
layout: single
title: Spring Boot 정리
categories: SPRING
tag: []
---

1. # 정리

   __@Configuration__   
   자바 스프링에서 설정 클래스를 지정하는 어노테이션입니다. 이 어노테이션이 붙은 클래스는 스프링 컨테이너에 의해 특별하게 처리되어, 해당 클래스 내에 정의된 **빈(Bean)**들을 스프링 컨테이너에 등록하고 관리하게 됩니다.   
   =>주로 Configuration을 설정한 클래스 안의 메소드에 bean설정   

   __@EnableWebSecurity__   
   어노테이션은 스프링 시큐리티를 사용하는 애플리케이션에서 웹 보안 설정을 활성화하는 데 사용되는 중요한 어노테이션입니다. 이 어노테이션이 붙은 클래스는 스프링 시큐리티의 기본적인 웹 보안 기능을 활용할 수 있도록 설정됩니다. 인증, 권한 부여, CSRF 보호 등 웹 애플리케이션에서 필요한 기본적인 보안 설정을 제공합니다.   

   __HttpSecurity__   
   스프링 시큐리티에서 웹 보안 설정을 위한 핵심 클래스입니다. 웹 애플리케이션에 대한 HTTP 요청을 보호하기 위한 다양한 기능을 제공하며, 이를 통해 인증, 권한 부여, CSRF 방지 등을 설정할 수 있습니다.   

   __http.build()__   
   HttpSecurity 객체를 빌드하여 스프링 시큐리티 필터 체인에 추가하는 역할을 합니다. 즉, 웹 보안 설정을 완료하고 실제로 적용하기 위한 마지막 단계라고 볼 수 있습니다.   

   __JWT 토큰이 전송되는 과정__   
   1)로그인 성공: 사용자가 처음 로그인에 성공하면, 서버는 JWT 토큰을 생성하여 클라이언트에게 전달합니다.
   2)토큰 저장: 클라이언트는 받은 JWT 토큰을 브라우저의 쿠키, 로컬 스토리지 등에 안전하게 저장합니다.
   3)다른 요청: 이후 클라이언트가 다른 페이지로 이동하거나 데이터를 요청할 때마다, 브라우저는 자동으로 저장된 JWT 토큰을 Authorization 헤더에 포함시켜 서버로 전송합니다.
   4)서버 검증: 서버는 받은 JWT 토큰의 유효성을 검증하고, 유효한 토큰이라면 사용자에게 허용된 자원에 대한 접근을 허용합니다.

   __스프링 부트에서 매개변수 위치에서 변수를 선언할 수 있는 이유__   
   스프링 부트에서 컨트롤러 메서드의 매개변수 자리에 변수를 직접 선언하여 사용할 수 있는 이유는 스프링의 강력한 의존성 주입(Dependency Injection) 기능과 타입 안전성 덕분입니다.   

   ```java
      @RestController
      public class MyController {

         @GetMapping("/hello")
         public String hello(User user) {
            // user 객체를 사용하여 로직 수행
            return "Hello, " + user.getName();
         }
      }
   ```   

   ```java
      @GetMapping("/search")
      public List<Product> searchProducts(@RequestParam String keyword) {
         // 서비스 계층에서 keyword를 이용하여 상품 검색
         List<Product> products = productService.search(keyword);
         return products;
      }

   ```

