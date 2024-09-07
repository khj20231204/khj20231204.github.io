---
layout: single
title: REST API와 Ajax
categories: SPRING
tag: []
author_profile: false
---

1. # REST API
   REST API: 서버에 있는 데이터를 클라이언트(웹 브라우저 등)에서 접근하고 조작할 수 있도록 제공하는 인터페이스입니다.   
   
1. # AJAX
   AJAX: 웹 페이지를 새로고침하지 않고 비동기적으로 서버와 통신하여 데이터를 주고받는 기술입니다.   
   REST API는 AJAX를 이용하여 구현될 수 있습니다. AJAX는 REST API를 호출하는 도구 중 하나입니다. 즉, REST API가 제공하는 기능을 사용하여 웹 페이지를 동적으로 만들 수 있습니다.   
   AJAX는 REST API뿐만 아니라 다른 방식의 서버 통신에도 사용될 수 있습니다. SOAP, GraphQL 등 다양한 방식의 서버 통신에 AJAX를 사용할 수 있습니다.   

   따라서 REST API는 AJAX를 포함하는 더 큰 개념이라고 할 수 있습니다.   

1. # JSON 전송
   Java Script Object Notation - 자바 스크립트 객체 표기법   
   예전 XML파일로 데이터를 주고 받았는데 XML표기법은 복잡하고 태그가 많아 불편함이 있었기 때문에 간단한 형식으로 데이터를 주고받기 위해서 개발되었습니다.   

   자바스크립트 객체를 서버로 전송하려면 HTTP 프로토콜을 이용해야 하기 때문에 text기반의 언어로 변환해야 합니다. 그렇기 때문에 직렬화 과정이 필요합니다. 객체도 메모리를 차지하고 있는 데이터이기 때문에 해당 데이터를 가져와서 문자화가 가능합니다.      
   __JSON.stringify() - 객체를 JSON 문자열로 변환(직렬화, JS객체 → 문자열)__   

   반대로, 데이터를 받은 측에서는 객체로 다시 변화해야 합니다. 객체를 생성 후 받은 문자열 데이터를 해당 객체에 삽입합니다. 이것이 역직렬화 입니다.   
   __JSON.parse() - JSON 문자열을 객체로 변환(역직렬화, 문자열 → JS객체)__   
   
   ```javascript
      JS객체 {name:"John", age:30} → JSON.stringify() → Stirng문자열 "{'name':'John','age':30}"
      JS객체 {name:"John", age:30} ← JSON.parse() ← String문자열 "{'name':'John','age':30}"
   ```   

   예제)   
   ```javascript
      let obj = {name:"kim", age:23}
      obj : {name: 'kim', age: 23, phone: '010-1234-1234'}  //obj 객체 생성

      let strObj = JSON.Stringify(obj);                     //Stringify
      strObj : '{"name":"kim","age":23,"phone":"010-1234-1234"}' //객체가 문자열로

      typeof obj
      'object'
      
      typeof strObj
      'string'
      
      let obj2 = JSON.parse(strObj);                        //parse
      obj2 : {name: 'kim', age: 23, phone: '010-1234-1234'} //문자열이 다시 객체로

      typeof obj2
      'object'
   ```
   
1. # Ajax
   Asynchronous Javascript and XML - 요즘은 JSON을 주로 사용   

   비동기 통신으로 데이터를 주고 받기 위한 기술   
   웹페이지 전체가 아닌 일부만 업데이트 가능   
   예)댓글을 다는 경우 전체 페이지가 리로딩되는 것이 아니라 댓글 부분만 추가됨   
   웹브라우저 - 탭 하나하나가 전부 싱글 스레드로 탭 사이에 응답을 기다리지 않는다  

   비동기시 처리 결과가 완료된 경우 콜백함수를 리턴해줍니다. 콜백함수는 비동기시 처리 결과를 알리는 함수이고 이렇게 작동하도록 설계된 것입니다.   
   *동기 - 기다린다   
   비동기 - 안 기다린다   

1. # jQuery를 이용한 Ajax   

   views 디렉토리에 있는 ajax.jsp파일 입니다.   
   ```javascript
      <%@ page contentType="text/html;charset=UTF-8" language="java" %>
      <html>
      <head>
         <title>Title</title>
         <script src="https://code.jquery.com/jquery-1.11.3.js"></script>
      </head>

      <body>
         <h2>{name:"abc", age:10}</h2>
         <button id="sendBtn" type="button">SEND</button>
         <h2>Data From Server :</h2>
         <div id="data"></div>
         <script>
            $(document).ready(function(){
                  let person = {name:"abc", age:10};
                  let person2 = {};

                  $("#sendBtn").click(function(){
                     $.ajax({
                        type:'POST',       // 요청 메서드
                        url: '/ch4/send',  // 요청 URI
                        headers : { "content-type": "application/json"}, // 요청 헤더
                        dataType : 'text', // 전송받을 데이터의 타입
                        data : JSON.stringify(person),  // 서버로 전송할 데이터. stringify()로 직렬화 필요.
                        success : function(result){
                              person2 = JSON.parse(result);    // 서버로부터 응답이 도착하면 호출될 함수
                              alert("received="+result);       // result는 서버가 전송한 데이터
                              $("#data").html("name="+person2.name+", age="+person2.age);
                        },
                        error   : function(){ alert("error") } // 에러가 발생했을 때, 호출될 함수
                     }); // $.ajax()

                     alert("the request is sent")
                  });
            });
         </script>
      </body>
      </html>
   ```
   데이터를 보낼 땐 stringify, 받은 데이터는 paring   
   데이터를 서버쪽에 전송할 때 success와 error라는 콜백함수를 같이 넘겨줍니다.   
   
   SEND 버튼을 클릭하면 '/ch4/send'로 data에 있는 person객체를 stringify해서 보내게 됩니다. 

   Controller   
   '/send'쪽의 @ResponseBody 와 @RequestBody는 필수입니다. POST방식은 Body에 데이터가 존재하기 때문입니다. get방식과 post방식 모두 Http프로토콜 양식을 따르기 때문에 status/header/공백/body의 순서로 프레임이 짜져있지만 get방식으로 데이터가 노출되어 있기 때문에 body를 따로 참조할 필요가 없지만 post방식은 body에 데이터가 있기 때문에 클라이언트에서 전송한 데이터는 RequestBody에 존재하고, 서버에서 전송할 데이터는 ResponseBody에 존재합니다.   

   __리턴타입__ 이 MVC에서는 뷰이름이지만 __ajax로 넘겨줄 때는 객체이름__ 이 됩니다. 꼭 객체일 필요는 없고, List나 Map을 리턴해도 jacksond-databind가 알아서 바꿔줍니다.   
   ```java
      import org.springframework.stereotype.Controller;
      import org.springframework.web.bind.annotation.*;

      import com.ch4.domain.Person;

      @Controller
      public class SimpleRestController {

         @GetMapping("/ajax")
         public String ajax() {
            return "ajax";
         }

         @PostMapping("/send")
         @ResponseBody  //@ResponseBody 필수, Controller에서 전송할 데이터의 body부분
         public Person test(@RequestBody Person p) {  //@RequestBody 필수, 클라이언트에서 전송한 데이터의 body부분
            System.out.println("p = " + p);
            p.setName("ABC");
            p.setAge(p.getAge() + 10);

            return p;
         }
      }
   ```
   Person이라는 이름의 클래스를 생성해 둬야합니다. 
   ajax에서 stringify를 이용해 문자로 변경한 데이터를 jackson-databind가 java객체로 변환합니다. 이 변환된 객체를 constroller의 RequestBody가 받습니다. Person이라는 객체를 받은 후 age에 10을 더한 후 리턴합니다. 리턴하면 /send를 호출한 ajax로 바로 데이터가 넘어갑니다. 이때 넘어가는 데이터는 역시 jackson-databind에 의해 문자열로 변환이 됩니다.    

   Person클래스   
   ```java   
      public class Person {
         private String name;
         private int age;
         
         public Person() {
            
         }
         
         public Person(String name, int age) {
            this.name = name;
            this.age = age;
         }
         
         public String getName() {
            return name;
         }
         
         public void setName(String name) {
            this.name = name;
         }
         
         public int getAge() {
            return age;
         }
         
         public void setAge(int age) {
            this.age = age;
         }

         @Override
         public String toString() {
            return "Person [name=" + name + ", age=" + age + "]";
         }
      }
   ```    

   요약 :   
   1."http://localhost/ch4/ajax" 경로로 ajax.jsp 예제 파일 로딩   
   2.버튼을 클릭하면 ajax에서 '/send'로 Person객체를 보냄   
   3.person객체가 stringify로 문자화 됨   
   4.서버의 jackson-databind에 의해 person문자열이 객체가 됨   
   5.자바 Controller의 '/send'에서 age를 10 증가   
   6.ajax로 다시 person객체를 리턴   
   7.jackson-databind에 의해 문자화   
   8.success에서 result로 데이터를 받은 후 parse 후 데이터 출력   

1. # RestController
   Rest API로 받은 데이터를 Contoller에서 전송할 때는 원래는 메소드마다 @ResponseBody를 붙여야하지만 클래스에 @RestController를 붙여서 메소드 마다 붙이는 @ResponseBody를 생략할 수 있습니다.   
   <span style="color:red">단, RestController를 사용시에는 해당 클래스 안에 메소드들이 전부 Post방식이여야 합니다.</span>   

1. # REST
   Roy Fielding이 제안한 웹서비스 디자인 아키텍쳐 접근 방식으로 프로토콜에 독립적이며, 주로 HTTP를 사용해서 구현합니다.   
   __리소스 중심__ 의 API 디자인입니다 - __HTTP 메서드로 수행할 작업__ 을 정의   

   => post, get, put, delete를 사용

1. # REST API
   REST가 정의한 설계 가이드를 잘 지키면 Rest API라고 합니다.   

   REST 가이드   
   1.자원기반 2.HTTP메소드 활용 3.무상태 4.캐싱 가능 5.클라이언트-서버 분리 6.계층화   

1. # RESTful API
   REST 규약 전부 준수하여 설계한 API입니다. 따라서 RESTful API는 같은 url 주소라도 get방식과 post방식에 따라 처리과정이 달라집니다.   
   