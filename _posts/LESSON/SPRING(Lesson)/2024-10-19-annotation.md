---
layout: single
title: 수업 시간에 다룬 주요 어노테이션
categories: SPRING(Lesson)
tag: []
author_profile: false
---
 
1. # @Controller
   @Controller 어노테이션은 Controller 기능을 수행 할 수 있도록 만들어 주는 역할을 합니다.   

   ```java
      @Controller
      public class HomeController {

         @RequestMapping(value = "/", method = RequestMethod.GET)
         public String home(Locale locale, Model model) {
            Date date = new Date();
            DateFormat dateFormat = DateFormat.getDateTimeInstance(DateFormat.LONG, DateFormat.LONG, locale);
            String formattedDate = dateFormat.format(date);
            model.addAttribute("serverTime", formattedDate );
            return "home";
         }
      }
   ```

1. # @RequestMapping
   @RequestMapping 어노테이션은 클라이언트의 요청을 받을때 사용하는 어노테이션입니다.   

   ```java
      @Controller
      public class HomeController {

         @RequestMapping(value = "/", method = RequestMethod.GET)
         public String home(Locale locale, Model model) {
            Date date = new Date();
            DateFormat dateFormat = DateFormat.getDateTimeInstance(DateFormat.LONG, DateFormat.LONG, locale);
            String formattedDate = dateFormat.format(date);
            model.addAttribute("serverTime", formattedDate );
            return "home";
         }
      }
   ```

1. # @RequestParam
   @RequestParam 어노테이션은 name 으로 값을 받을때 사용하는 어노테이션이다.   
   @RequestParam(“name”) 어노테이션은 request.getParameter(“name”)와 같은 역할을 한다   

   ```java
      @Controller
      public class HomeController {
         @RequestMapping(value = "/", method = RequestMethod.GET)
         public String home(@RequestParam(“name”) String name, Model model) {
         }
      }
   ```

1. # @ModelAttribute
   @ModelAttribute 어노테이션은 DTO클래스로 값을 받을때 사용하는 어노테이션이다.

   ```java
      @Controller
      public class HomeController {
         @RequestMapping(value = "/", method = RequestMethod.GET)
            public String home(@ModelAttribute BoardDTO board, Model model) {
         }
      }
   ```

1. # @Bean
   📌 어디에 사용?   
   개발자가 직접 객체(Bean)를 생성하고 Spring 컨테이너에 등록할 때 사용   
   @Configuration이 붙은 클래스 내부에서 메서드 단위로 Bean을 등록   
   🛠 예제: @Bean으로 PasswordEncoder 등록   

   ✅ 내가 직접 생성한 객체를 Bean으로 등록해야 할 때   
   예: PasswordEncoder, ModelMapper, RestTemplate   
   라이브러리에서 제공하는 클래스를 직접 등록해야 할 경우   

   ```java
     @Configuration
      public class AppConfig {
         
         @Bean
         public PasswordEncoder passwordEncoder() {
            return new BCryptPasswordEncoder(); // ✅ 직접 객체 생성 후 Bean 등록
         }
      }
   ```

1. # @Autowried
   📌 어디에 사용?   
   Spring 컨테이너에 이미 등록된 Bean을 주입(Inject)할 때 사용   
   필드, 생성자, 메서드에서 사용 가능   
   🛠 예제: @Autowired로 PasswordEncoder 주입   
   
   ✅ Spring이 관리하는 Bean을 가져와서 사용할 때    
   예: UserRepository, PasswordEncoder, Service, Component   
   이미 @Component, @Service, @Repository로 등록된 Bean을 주입받을 때   

   ```java
      @Service
      public class UserService {
         
         private final PasswordEncoder passwordEncoder;

         @Autowired
         public UserService(PasswordEncoder passwordEncoder) { // ✅ Bean을 주입받음
            this.passwordEncoder = passwordEncoder;
         }

         public void registerUser(String password) {
            String encodedPassword = passwordEncoder.encode(password);
            System.out.println("암호화된 비밀번호: " + encodedPassword);
         }
      }
   ```

   __@Bean vs @Autowried__   
   @Bean - @Configuration 안에서   
   @Autowried - @@Component, @Service, @Repository 안에서   