---
layout: single
title: Spring Boot Security정리
categories: SPRINGBOOT
tag: []
---

1. # 정리

   __@Configuration__   
   자바 스프링에서 설정 클래스를 지정하는 어노테이션입니다. 이 어노테이션이 붙은 클래스는 스프링 컨테이너에 의해 특별하게 처리되어, 해당 클래스 내에 정의된 **빈(Bean)**들을 스프링 컨테이너에 등록하고 관리하게 됩니다.   
   =>주로 Configuration을 설정한 클래스 안의 메소드에 bean설정   
   사용 예)   
   ```java   
      @Configuration
      public class AppConfig {

         @Bean
         public MyService myService() {
            return new MyService();
         }
      }
   ```

   __@Component__   
   스프링 부트 애플리케이션에서 Bean을 정의하는 데 사용되는 표준 메커니즘입니다. 스프링 컨테이너가 애플리케이션을 시작할 때, @Component 애노테이션이 붙은 클래스를 자동으로 검색하고 Bean으로 등록합니다. 클래스에 Component를 붙이면 다른 클래스에서 Autowired로 의존성을 주입하여 해당 클래스를 사용할 수 있습니다.   

   -JwtProp.java-   
   ```java
      @Component 
      public class JwtProp {
         private String secretKey;
      }
   ```   
   JwtProp.java에서 Component로 선언하면 LoginController에서 JwtProp클래스에 Autowired를 주입 후 사용 가능   
   -LoginController.java-   
   ```java
      public class LoginController {

         @Autowired //의존성 주입
         private JwtProp jwtProp; //JwtProp 사용 가능
      }
   ```

   =>   
   @Component(컴포넌트임을 선언) : 바로 빈으로 등록   
   @Configuration(설정 선언) : @Bean을 사용하여 빈으로 등록   

   __@ConfigurationProperties("com.hjcompany.jwt")__   
   com.hjcompany.jwt 경로 하위 속성들을 지정   
   ```java
      @ConfigurationProperties(prefix = "my.app")
      @Component
      public class MyAppProperties {
         private String serverUrl;
         private int port;
         // ... getter, setter
      }
   ```
   properties 파일 (application.properties, application.yml)에 정의된 값을 Java Bean의 속성에 자동으로 바인딩합니다.   
   application.properties 파일에 정의된 my.app으로 시작하는 설정 값들을 MyAppProperties 클래스에 바인딩하고, 이 클래스를 @Component에 의해 스프링 컨테이너에 Bean으로 등록합니다.

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

   __@Slf4j__   
   에러나 간단한 정보, 버그시 로그를 남길 때 사용하는 어노테이션   

   __ResponseEntity__   
   스프링 프레임워크에서 HTTP 응답을 나타내는 클래스입니다. 단순히 데이터만 반환하는 것이 아니라, HTTP 상태 코드, 헤더, 본문 등 다양한 정보를 포함하여 클라이언트에게 더욱 풍부한 응답을 제공할 수 있도록 해줍니다.

   __claim__   
   JWT(JSON Web Token)에서 Claim은 토큰 내에 포함된 사용자 정보나 메타데이터를 의미합니다. 이 주장들은 JSON 형태로 표현되며, 토큰의 유효성 검증이나 사용자 식별 등에 활용됩니다.   

   claim 예시   
   ```json
      {
         "iss": "https://example.com",
         "sub": "user123",
         "name": "John Doe",
         "admin": true,
         "iat": 1516239022
      }
   ```