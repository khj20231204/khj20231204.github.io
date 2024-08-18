---
layout: single
title: 브라우저와 WAS의 연결과정
categories: SPRING
tag: []
author_profile: false
---

1. # 원격 실행
   브라우저에서 서버로 명령을 전달하고 서버에 있는 명령이 실행되는 원격으로 이루어지는 과정입니다. 서버와 클라이언트 간에 명령을 주고 받을 수 있는 원격 실행이 가능한 이유는 WAS와 같은 웹애플리케이션 서버가 있기 때문에 가능합니다. 먼저 프로그램을 WAS에 등록을 시키고, 그 다음 URL과 프로그램을 연결해야합니다.   
   
   1)프로그램 등록 : @Controller 이용      
   2)URL과 프로그램 연결 : @RequestMapping이용   

   ```java
      @Controller //1. 프로그램 등록
      public class Hello {
         
         @RequestMapping("/hello")  //2. URL과 main() 연결
         public void main(){        //hello 주소와 main을 연결
            System.out.println("Hello");
         }
   }
   ```   
   예를 들어 `http://111.222.333.444:8080/ch2/hello` 다음과 같은 주소로 위를 호출 할 때 URL의 마지막 hello라는 주소값이 RequestMapping 주소값과 같습니다. http://111.222.333.444:8080는 주소와 포트번호입니다. ch2는 Context root입니다.   
   메소드 main이란 이름은 중요하지 않습니다. RequestMapping 아래에 있는 메소드가 주소이름과 맵핑됩니다. main이란 이름대신 다른 이름으로 사용해도 됩니다.   
   
   