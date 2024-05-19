---
layout: single
title: JAVA Spring
categories: Interview
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

1. # @RequestMapping의 단축 어노테이션
   Spring은 GET, POST, PUT, DELETE, PATCH 와 같은 수신 HTTP 요청 메소드를 처리하기 위해 다음과 같은 5가지 어노테이션을 제공한다.    
   @GetMapping   
   @PostMapping   
   @PutMapping   
   @DeleteMapping   
   @PatchMapping   

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
   클라이언트가 전송하는 HTTP parameter, Body 내용을 Setter 함수를 통해 1:1로 객체에 데이터를 연결(바인딩)합니다

1. # @Autowired   
   의존성을 주입받는 방법

1. # 의존성 주입 방법
   생성자 주입 - 생성자에 @Autowired를 붙여준다   
   수정자 주입 (setter 주입) - setter메소드 위에 @Autowired를 붙여준다   
   필드 주입 - 필드 맴버 객체 위에 @Autowired를 붙여준다      

1. # Model 객체
   Controller에서 생성된 데이터를 담아 view로 전달할 때 사용하는 객체.   
   servlet의 request.setAttribute()와 비슷한 역할을 함

1. # Entity Class
   Entity 클래스는 실제 DB 테이블과 매핑되는 핵심 클래스로, 데이터베이스의 테이블에 존재하는 컬럼들을 필드로 가지는 객체입니다. (DB의 테이블과 1:1로 매핑되며, 테이블이 가지지 않는 컬럼을 필드로 가져서는 안 됩니다.)   

1. # 스프링 컨텍스트
   스프링이 관리하는 빈들이 담겨있는 컨테이너   
   -ROOT-CONTEXT(공통 부분)   
   모든 서블릿이 공유할 수 있는 Bean들이 모인 공간. DB와 관련된 Repository, Service 등이 있음.   
   -SERVLET-CONTEXT(개별 부분)   
   서블릿 각자의 Bean들이 모인 공간. 웹, 앱 마다 한 개씩 존재하므로 웹 앱 그 자체를 의미하기도 함. 이 Context 내에서의 Bean들은 서로 공유될 수 없음. MVC의 Controller가 이에 해당

1. # ORM
   Object Relation Mapping의 약자로 객체(자바)-관계(DB)의 맵핑이다. 객체와 관계형 데이터베이스의 데이터를 자동으로 맵핑.   

1. # API
   ```css
      https://api.openweathermap.org/data/3.0/onecall?lat={lat}&lon={lon}&exclude={part}&appid={API key}

      {
         "lat":33.44,
         "lon":-94.04,
         "timezone":"America/Chicago",
         "timezone_offset":-18000,
         "current":{
            "dt":1684929490,
            "sunrise":1684926645,
            "sunset":1684977332,
            "temp":292.55,
            "feels_like":292.87,
            "pressure":1014,
            "humidity":89,
            "dew_point":290.69,
            "uvi":0.16,
            "clouds":53,
            "visibility":10000,
            "wind_speed":3.13,
            "wind_deg":93,
            "wind_gust":6.71,
            "weather":[
               {
                  "id":803,
                  "main":"Clouds",
                  "description":"broken clouds",
                  "icon":"04d"
               }
            ]
         },
      }
   ```
   Application Programming Interface의 약자로 애플리케이션 개발에서 다른 서비스에 요청을 보내고 응답을 받기 위해 정의된 명세를 일컫는다. 서버가 제공하는 서비스를 클라이언트가 이용한다 했을 때 어떤어떤 방식으로 데이터를 주고 받을지 정해놓은 메뉴판 같은 것

1. # REST API 주소 방식   
   POST https://api.backets.com/v1/goods --- Create   
   GET https://api.backets.com/v1/goods --- Read   
   GET  https://api.backets.com/v1/goods/1 --- Read   
   PUT  https://api.backets.com/v1/goods/14 --- Update(전체 수정)   
   PATCH  https://api.backets.com/v1/goods/27 --- Update(부분 수정)   
   DELETE  https://api.backets.com/v1/goods/34 --- Delete   

   REST : REpresentational State Transfer(주고받는) 자원을 이름(자원의 표현)으로 구분해 상태를 주고받는다

1. # RESTful API
   *ful ~한다, ~스럽다   
   RESTful REST한다, REST스럽다   
   REST의 설계 규칙을 잘 지켜서 설계된 API를 RESTful API라고 합니다. REST의 원리를 잘 따르는 시스템. 잘 만들어진 데이터가 있으면 요청과 응답이 체계적으로 이루어질 수 있다   

   *설계 규칙   
   1)의미를 바로 알아볼 수 있도록 작성하고, 소문자를 사용한다.   
   ❌ GET /users/writing   
   ❌ GET /users/Post-Comments   
   ⭕ GET /users/post-comments   

   2)URI가 길어지는 경우 언더바(_) 대신 하이픈(-)을 사용한다.   
   ❌ GET /users/profile_image   
   ⭕ GET /users/profile-image   

   3)마지막에 슬래시(/)를 포함하지 않는다.   
   후행 슬래시(/)는 의미가 전혀 없고 혼란을 야기할 수 있다.   
   ❌ GET /users/   
   ⭕ GET /users   

   4)리소스에 대한 행위를 HTTP Method로 표현한다.    
   -URI에 HTTP Method가 포함되서는 안된다.   
   ❌ get/users/   
   ⭕ GET /users/   
   -resource는 동사가 포함되서는 안되고 명사를 사용한다.   
   ❌ GET /users/show/1   
   ⭕ GET /users/1   
   
   5)파일 확장자는 URI에 포함시키지 않는다.   
   ❌ GET /users/photo.jpg   
   ⭕ GET /users/photo (이때, payload의 포맷은 headers에 accept를 사용한다.)   

   6)URI 사이에 연관 관계가 있는 경우 /리소스/고유ID/관계 있는 리소스 순으로 작성한다.   
   ❌ GET /users/profile/{user_id}   
   ⭕ GET /users/{user_id}/profile   

   7)URI에 작성되는 영어를 복수형으로 작성한다.   
   ❌ GET /product   
   ⭕ GET /products   

   8)URI는 / 구분자를 사용하여 자원의 계층 관계를 나타내는데 사용한다.

1. # 스프링 3대 요소
   1)IoC/DI(제어의 역전/의존성 주입)   
   2)AOP(관점 지향 프로그래밍)   
   3)PSA(서비스 추상화):환경의 변화와 상관없이 일관된 방식의 기술로 접근 환경을 제공하는 추상화 구조이다. 특정 환경이나 서버에 종속되지 않은 애플리케이션을 개발할 수 있다.   

1. # Bean Validation 어노테이션의 종류
   @AssertFalse - False일 경우   
   @AssertTrue - True일 경우   
   @DecimalMax(value=) - 지정 값 이하 실수   
   @DecimalMin(value=) - 지정 값 이상 실수   
   @Digits(integer=,fraction=) - 속성 값이 지정된 정수화 소수 자리수보다 적을 경우   
   @Future - 속성 날짜가 현재보다 미래인 경우   
   @Past - 속성 날짜가 현재보다 과거인 경우   
   @Max(value) - 지정 값이하인 경우   
   @Min(value) - 지정 값이상인 경우   
   @NotNull - 널이 아닌 경우   
   @Null - 널인 경우   
   @Pattern(regex=, flag=) - 해당 정규식 통과인 경우   
   @Size(min=, max=) - 문자열 또는 배열이 지정값 사이인 경우   
   @Valid - 확인 조건 만족한 경우   

   
   

