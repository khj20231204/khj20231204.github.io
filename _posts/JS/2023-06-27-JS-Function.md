---
layout: single
title: 함수 정의하기
categories: JS
tag: [함수 선언, 화살표함수]
---

1. # 함수를 정의하는 방법
   1. ## 함수 선언문으로 정의하는 방법
      ```js
         function f(x) { return x*x; }
      ```
   1. ## 함수 리터럴로 정의하는 방법
      ```js
         var f = function(x) { return x*x; }
      ```
   1. ## Function 생성자로 정의하는 방법
      ```js
         var f = new Funcion("x","return x*x");
      ```   
      Function은 함수를 생성하는 내장 생성자입니다.   
      ```
         var 변수 이름 = new Function(첫 번째 인수, ... , n번째 인수 , 함수 몸통)   
      ```   
      function으로 생성한 함수는 전역 변수와 자신의 지역 변수만 읽고 쓸 수 있다는 단점이 있습니다. 그렇기 때문에 함수를 동적으로 생성해야하는 특별한 상황 외에는 잘 사용하지 않습니다. 또한 보안에도 문제가 있기 때문에 함수를 생성하기 위해 사용한다기 보다는 함수 리터럴에 래퍼 객체를 제공한다는 점에 의미를 줄 수 있습니다.   

1. # 화살표 함수 표현식으로 정의하는 방법
   ```js
      var f = x => x*x;
   ```  
   <br/>
   함수 선언문으로 정의한 함수는   

   >.. 함수 호출 ..  
   .. 함수 정의 ..   

   처럼 함수 정의 이전에 호출하는 것이 가능 합니다. 자바스크립트 엔진이 함수 선언문을 프로그램의 첫머리로 끌어올리기 때문입니다.   
   하지만 2)함수 리터럴, 3)Function생성자, 4)화살표 함수로 정의된 함수는 <span style="color:red">변수에 참조를 할당</span>해야 비로소 사용할 수 있기 때문에 함수 호출이 반드시 함수 정의 이후에 이루어져야 합니다.

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

1. # 중첩 함수
   자바스크립트는 외부 함수의 최상위 레벨에서만 중첩 함수를 사용할 수 있습니다. 함수 안의 if문이나 while문 등 문장 블록 안에서는 사용할 수 없습니다.   

   ```js
      // 중첩 함수
      function square(t){
         var tot = sum();
         console.log("tot:"+tot);

         function sum(){
            console.log(t);
            var tot = 0;
            for(var i=0 ; i<t.length ; i++){
              tot += t[i]*t[i]
            }
            return tot;
         }
      }

      let array = [1,2,3];
      squer(array);
   ```   
   square함수 내부에 sum함수가 있습니다. sum의 결과값을 받아서 square함수 안에서 출력합니다.   

1. # 함수를 호출하는 방법
