---
layout: single
title: REST API와 Ajax
categories: SPRING
tag: []
author_profile: false
---

1. # REST API
   REST API: 서버에 있는 데이터를 클라이언트(웹 브라우저 등)에서 접근하고 조작할 수 있도록 제공하는 인터페이스입니다.
   AJAX: 웹 페이지를 새로고침하지 않고 비동기적으로 서버와 통신하여 데이터를 주고받는 기술입니다.
   REST API는 AJAX를 이용하여 구현될 수 있습니다. AJAX는 REST API를 호출하는 도구 중 하나입니다. 즉, REST API가 제공하는 기능을 사용하여 웹 페이지를 동적으로 만들 수 있습니다.
AJAX는 REST API뿐만 아니라 다른 방식의 서버 통신에도 사용될 수 있습니다. SOAP, GraphQL 등 다양한 방식의 서버 통신에 AJAX를 사용할 수 있습니다.

따라서 REST API는 AJAX를 포함하는 더 큰 개념이라고 할 수 있습니다.


1. # JSON 전송
   Java Script Object Notation - 자바 스크립트 객체 표기법   
   예전 XML파일로 데이터를 주고 받았는데 XML표기법은 복잡하고 태그가 많아 불편함이 있었기 때문에 간단한 형식으로 데이터를 주고받기 위해서 개발되었습니다.   

   자바스크립트 객체를 서버로 전송하려면 HTTP 프로토콜을 이용해야 하기 때문에 text기반의 언어로 변환해야 합니다. 그렇기 때문에 직렬화 과정이 필요합니다.   
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
   ```javascript
      $(document).ready({

         let person = {name:"abc", age:10};
         let person2 = {};

         $("sendData").click(function(){

            $.ajax({
               type : 'POST',  //요청 메서드
               url : 'ch4/send',   //요청 url
               headers : {"content-type":"application/json"},
               dataType : 'text' , //전송할 데이터 타입
               data : JSON.stringify(person) //서버로 전송할 데이터. stringify()로 직렬화 필요

               //success와 error가 콜백함수
               success : function(data){
                  person2 = JSON.parse(data); //받고 나서는 parse()로 역직렬화
               },
               error : function(){
                  console.log("error");
               }
            }); //$.ajax()

            alert("the request is sent"); //비동기 방식이기 때문에 ajax의 결과를 얻지 않았지만 바로 alert가 실행됨. 
         })
      });
   ```
   데이터를 보낼 땐 stringify, 받은 데이터는 paring   
   데이터를 서버쪽에 전송할 때 success와 error라는 콜백함수를 같이 넘겨줍니다.   

jsp에서 ch/04 주소로 ajax -> 자바 Controller, Mapping("ch/04") -> ajax의 success로 받는다