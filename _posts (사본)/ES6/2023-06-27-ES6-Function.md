---
layout: single
title: 함수 정의하기
categories: ES6
tag: [함수 선언, 화살표함수]
---

1. ## 함수를 정의하는 방법
   1. ### 함수 선언문으로 정의하는 방법
   ```javascript
      function f(x) { return x*x; }
   ```
   1. ### 함수 리터럴로 정의하는 방법
   ```javascript
      var f = function(x) { return x*x; }
   ```
   1. ### Function 생성자로 정의하는 방법
   ```javascript
      var f = new Funcion("x","return x*x");
   ```
   1. ### 화살표 함수 표현식으로 정의하는 방법
   ```javascript
      var f = x => x*x;
   ```  
   <br/>
함수 선언문으로 정의한 함수는   

   >.. 함수 호출 ..  
   .. 함수 정의 ..   

   처럼 함수 정의 이전에 호출하는 것이 가능 합니다. 자바스크립트 엔진이 함수 선언문을 프로그램의 첫머리로 끌어올리기 때문입니다.   
   하지만 2)함수 리터럴, 3)Function생성자, 4)화살표 함수로 정의된 함수는 <span style="color:red">변수에 참조를 할당</span>해야 비로소 사용할 수 있기 때문에 함수 호출이 반드시 함수 정의 이후에 이루어져야 합니다.

1. ## 작성 중..