---
layout: single
title: 함수와 화살표 함수
categories: JS
tag: []
---
 
 1. # 함수
   ```js
      function sayHello(name){
         console.log(name); 
         let msg = 'Hello, ';
         if(name){
            msg += `${name}`;
            //msg += ${name};
         }

         console.log(msg);
      }

      sayHello(); 
      
      sayHello("ddochi");
   ```   
   `${name}`을 사용하려면 `msg += ${name}` 로 바로 사용하지 못 하고 반드시 \` \` 안에서 `${}`를 사용해야 합니다.   

   sayHello();   
   console.log(name); //undefined   
   변수 name에 아무런 값이 없기 때문에 undefined가 발생합니다. undefined는 boolean으로 false입니다.   

1. # 함수 선언문과 함수 표현식
   ```js
      //***함수 선언문***
      function sayHello1(){  //선언
         ...
      }
      sayHello1(); //호출

      //***함수 표현식***
      let sayHello2 = function(){  //선언
         ...
      }
      sayHello2(); //호출
   ```   
   함수 선언문과 표현식은 둘 다 사용방법과 호출방법은 같습니다. 차이점은 호출할 수 있는 타이밍입니다.   

   __함수 선언문 : 어디서는 호출 가능__   
   함수 선언문은 어디서든 호출 가능합니다.   
   ```js
      sayHello1(); //호출
      
      function sayHello1(){  //선언
         ...
      }
   ```   
   호출을 선언 이전에 해도 가능합니다.   
   만약 일반 변수가 선언과 호출의 순서가 바뀐다면,
   ```js
      console.log(num); //error발생
      let num = 1; //선언
   ```   
   선언 이전에 console에서 num변수를 호출하고 있기 때문에 error가 발생합니다.   

   함수 선언문이 어디서든 실행가능한 이유는 호스이스팅 덕분입니다.   

   __함수 표현식 : 코드에 도달하면 생성__
   ```js
      sayHello(); //선언 전에 호출 error 발생

      let sayHello = function(){ //함수 표현식 선언
         ...
      }
   ```   
   함수 표현식은 선언 이전에 호출을 하게되면 error가 발생합니다.   

1. # 화살표 함수
   ```js
      //표현식
      let add = function(num1, num2){
         return num1+num2;
      }

      //화살표 함수, function이 없어지고 => 가 생김
      let add = (num1, num2) => {
         return num1+num2;
      }

      let age = (num) => `your age is ${num}`;

      let age = num => `your age is ${num}`;

      let showError = () => {
         alert('error');
      }


   ```