---
layout: single
title: 부트 어노테이션과 인터페이스 
categories: SPRINGBOOT
tag: []
---


1. # 어노테이션

   __스테레오타입 어노테이션__   
   클래스의 역할이나 목적을 명확하게 나타내기 위해 사용하는 메타데이터입니다. 마치 사람에게 직업이나 역할을 부여하는 명찰과 같이, 스프링 프레임워크에서는 클래스에 어떤 역할을 부여할 것인지 명시적으로 알려주는 역할을 합니다.

   주요 스테레오타입 어노테이션   
   ```
      @Component: 가장 일반적인 어노테이션으로, 스프링 컨테이너에 빈으로 등록할 일반적인 클래스를 나타냅니다.
      @Service: 서비스 계층의 빈을 나타냅니다. 주로 비즈니스 로직을 담당하는 클래스에 사용됩니다.
      @Repository: 데이터 접근 계층의 빈을 나타냅니다. 주로 데이터베이스와 상호작용하는 클래스에 사용됩니다.
      @Controller: 웹 계층의 빈을 나타냅니다. 스프링 MVC에서 컨트롤러 역할을 하는 클래스에 사용됩니다.
   ```

   예)   
   ```java
      @Service
      public class UserService {
         // 사용자 관련 비즈니스 로직
      }

      @Repository
      public interface UserRepository extends JpaRepository<User, Long> {
         // 사용자 데이터 접근 로직
      }
   ```
   UserService는 서비스 계층의 빈이고, UserRepository는 데이터 접근 계층의 빈임을 명확하게 나타냅니다.   

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

1. # 클래스/메소드/인터페이스

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

   __ResponseEntity__   
   스프링 프레임워크에서 HTTP 응답을 나타내는 클래스입니다. 단순히 데이터만 반환하는 것이 아니라, HTTP 상태 코드, 헤더, 본문 등 다양한 정보를 포함하여 클라이언트에게 더욱 풍부한 응답을 제공할 수 있도록 해줍니다.   
   RESTful API를 개발할 때, 클라이언트에게 다양한 정보를 전달해야 할 경우 ResponseEntity를 사용하면 매우 유용합니다. 예를 들어, 요청이 성공했는지 실패했는지, 에러 메시지, 추가적인 헤더 정보 등을 함께 전달할 수 있습니다.   
   
   예제)   
   ```java
      public ResponseEntity<?> join(@RequestBody Users user) throws Exception {

         ...

         return new ResponseEntity<>("SUCCUESS",HttpStatus.OK);
      }
   ```

   __UserDetails 인터페이스__   
   스프링 시큐리티에서 사용자 정보를 담는 인터페이스입니다. 사용자의 권한, 비밀번호, 사용자 이름 등을 포함하여 사용자 인증에 필요한 모든 정보를 담고 있습니다. 즉, 시스템에 접근하려는 사용자를 나타내는 객체라고 할 수 있습니다.   

   UserDetails 인터페이스의 주요 메소드   
   ```
      getUsername(): String: 로그인 ID를 반환
      getPassword(): String: 암호를 반환
      getAuthorities(): Collection<? extends GrantedAuthority>: 사용자가 가지고 있는 권한 목록을 반환
      isEnabled(): boolean: 계정이 활성화되어 있는지 여부를 반환
      isAccountNonExpired(): boolean: 계정이 만료되지 않았는지 여부를 반환
      isCredentialsNonExpired(): boolean: 비밀번호가 만료되지 않았는지 여부를 반환
      isAccountNonLocked(): boolean: 계정이 잠기지 않았는지 여부를 반환
   ```

1. # 시큐리티
   __AuthenticationManager__   
   스프링 시큐리티에서 사용자 인증을 책임지는 핵심 인터페이스입니다. 사용자의 신원을 확인하고, 해당 사용자에게 부여할 권한을 결정하는 역할을 합니다. AuthenticationManager는 사용자가 시스템에 접근하려고 할 때, 제공된 정보(주로 아이디와 비밀번호)가 유효한지 검증하고, 만약 유효하다면 해당 사용자에게 어떤 권한을 부여할지를 결정하는 역할을 합니다.   

   __Authentication__   
   사용자가 시스템에 접근하려 할 때, 해당 사용자의 신원을 확인하고 인증하는 과정을 의미합니다. 즉, "당신이 누구인가?" 라는 질문에 대한 답을 찾는 과정이라고 할 수 있습니다.   

   __JwtAuthenticationFilter__   
   Spring Security에서 JWT(JSON Web Token) 기반 인증을 처리하는 필터입니다. 클라이언트가 요청할 때마다 실행되어, 요청 헤더에 포함된 JWT 토큰의 유효성을 검증하고, 유효한 토큰인 경우 인증된 사용자 정보를 SecurityContext에 설정하여 후속 요청에 대한 권한 검사를 가능하게 합니다.   

   __@EnableWebSecurity__   
   스프링 시큐리티(Spring Security)를 사용하는 스프링 부트 애플리케이션에서 필수적인 어노테이션입니다. 이 어노테이션은 해당 클래스에서 웹 보안 설정을 활성화한다는 것을 의미합니다. 즉, 스프링 시큐리티의 다양한 기능들을 사용하여 애플리케이션을 보호할 수 있도록 환경을 마련해 주는 것입니다.   

   __@EnableMethodSecurity__   
   스프링 시큐리티(Spring Security)에서 메서드 레벨의 보안 설정을 활성화하는 데 사용됩니다. 즉, 특정 메서드에 대한 접근 권한을 세밀하게 제어할 수 있도록 해줍니다.   
      prePostEnabled=true:   
         pre: 메서드 실행 전에 권한을 검사할 수 있도록 합니다.   
         post: 메서드 실행 후에 권한을 검사할 수 있도록 합니다.   
      securedEnabled=true:   
      메서드에 대한 접근 권한을 제어하기 위해 @Secured 어노테이션을 사용할 수 있도록 허용한다는 의미입니다.   

   __OncePerRequestFilter__   
   한 요청당 한 번만 실행되는 필터입니다. 즉, 한 번의 요청에 대해 여러 번 호출되는 것을 방지하여 불필요한 자원 낭비를 줄이고, 예상치 못한 동작을 방지하는 역할을 합니다.   

   __filterChain.doFilter__   
   이 메서드를 호출하면 현재 필터를 포함하여 필터 체인에 등록된 모든 필터들이 순서대로 실행되도록 합니다.

   __HttpSecurity__   
   스프링 시큐리티에서 웹 보안 설정을 위한 핵심 클래스입니다. 웹 애플리케이션에 대한 HTTP 요청을 보호하기 위한 다양한 기능을 제공하며, 이를 통해 인증, 권한 부여, CSRF 방지 등을 설정할 수 있습니다.   

   __http.build()__   
   HttpSecurity 객체를 빌드하여 스프링 시큐리티 필터 체인에 추가하는 역할을 합니다. 즉, 웹 보안 설정을 완료하고 실제로 적용하기 위한 마지막 단계라고 볼 수 있습니다.   
ㅂ
   __@Slf4j__   
   에러나 간단한 정보, 버그시 로그를 남길 때 사용하는 어노테이션   


1. # JWT
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

    __JWT 토큰이 전송되는 과정__   
   1)로그인 성공: 사용자가 처음 로그인에 성공하면, 서버는 JWT 토큰을 생성하여 클라이언트에게 전달합니다.
   2)토큰 저장: 클라이언트는 받은 JWT 토큰을 브라우저의 쿠키, 로컬 스토리지 등에 안전하게 저장합니다.
   3)다른 요청: 이후 클라이언트가 다른 페이지로 이동하거나 데이터를 요청할 때마다, 브라우저는 자동으로 저장된 JWT 토큰을 Authorization 헤더에 포함시켜 서버로 전송합니다.
   4)서버 검증: 서버는 받은 JWT 토큰의 유효성을 검증하고, 유효한 토큰이라면 사용자에게 허용된 자원에 대한 접근을 허용합니다.