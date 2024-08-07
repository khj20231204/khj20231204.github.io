---
layout: single
title: 클로져
categories: JS
tag: []
---
 
1. # 클로져
   함수가 생성되면서 만들어지는 렉시컬환경과 그 함수와의 결합, 조합입니다. 함수가 생성될 당시의 변수 환경을 기억하고, 그 환경에 접근할 수 있는 특별한 객체입니다.   

   ```
      lexcialEnviroment와 내부함수의 조합
   ```

   실행 컨텍스트A 내부에서 함수B를 선언한 경우   
   :A의'LexicalEnviroment'와 함수B의 조합에서 나타나는 특별한 현상 => 클로져   

   클로져를 이용하여 지역변수가 함수 종료 후에도 메모리를 계속 차지하여 함수 종료 후에도 사라지지 않는 지역변수를 만들 수 있습니다. 함수 생성시 자동으로 생성되는 개념이지만 클로져의 사용은 특별한 경우에 활용을 하게됩니다.   

   ```js
      function A(){};
      var v = A();   //A함수 호출로 return값을 받게 됩니다.
      var v = A;     //A함수 자체로 참조값이 변수v에 입력됩니다.
   ```   
   A() : 함수 리턴값   
   A : 함수A 자체   

   클로져 예제)   
   ```js
      function A() {
         function B() {
            console.log("b");
         }

         return B; //함수B 자체를 리턴, 함수B의 참조 값을 리턴
      }

      var v = A(); //A함수를 호출, 함수B를 받음
      //변수 v가 함수B가 됨

      v(); //함수 B호출
   ```

1. # 결과값을 리턴과 함수 자체를 대입
   ```js
      function makeCounter(){
         var count = 0;

         return f; //함수f 자체

         function f(){
            return count++;
         }
      }

      var counter = makeCounter(); //호출 결과 return값, 함수f 자체를 리턴
      var counter2 = makeCounter; //함수makeCounter자체를 참조
      
      console.log(counter()); //makeCounter()함수의 호출 결과값 함수f를 호출
      //0

      console.log(counter()); 
      //1

      console.log(counter);   //makeCounter()호출한 결과 값으로 받은 함수f 자체
      /*
      ƒ f(){
            return count++;
         }
      */

      console.log(counter2()); //makeCounter함수 자체를 변수 counter2에 대입, counter2호출
      /*
      ƒ f(){
            return count++;
         }
      */

      console.log(counter2);  //makeConter함수 자체 출력
      /*
      ƒ makeCounter(){
         var count = 0;

         return f; 

         function f(){
            return count++;
         }
      }*/
   ```
