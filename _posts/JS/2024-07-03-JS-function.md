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

1. # 함수 선언문
   ```js
      //***함수 선언문***
      function sayHello1(){  //선언
         ...
      }
      sayHello1(); //호출
   ```

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

1. # 함수 표현식
   함수 리터럴로 생성한 함수 객체를 변수에 할당하는 방식을 함수 표현식이라고 합니다.   

   ```js
      //***함수 표현식***
      let sayHello2 = function(){  //선언
         ...
      }
      sayHello2(); //호출
   ```   
   function() { ... } : 함수리터럴 = 익명함수 = 무명함수   
   함수 리터럴로 생성한 객체를 sayHello2의 변수에 할당.   
   =>  함수 리터럴로 생성한 함수 객체

   함수 표현식은 선언 이전에 호출을 하게되면 error가 발생합니다.   

   function(X){...} 이 부분이 함수 리터럴입니다. 함수 리터럴은 이름이 없는 함수이므로 익명 함수 또는 무명 함수라고 부릅니다.   
   함수 선언문에서는 끝에 ;를 붙일 필요가 없지만 함수 리터럴을 사용할 때는 끝에 세미콜론을 붙여야 합니다.

1. # 함수 선언문과 함수 표현식의 차이점
   함수 선언문과 표현식은 둘 다 사용방법과 호출방법은 같습니다. 차이점은 호출할 수 있는 타이밍입니다.   
   자바스크립트 엔진이 선언문으로 정의된 함수는 끌어올리지만, 리터럴로 정의된 함수는 끌어올리지 않는다는 차이가 있습니다.  

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

1. # 매개변수로 객체 사용
   ```js
      let obj = {
         name : "kim",
         age : 23
      };

      function setBall(v){
         console.log(v.name + " " +v.age);
      }

      setBall(obj);  //kim 23
   ```   

