---
layout: single
title: 객체 확장 표현식
categories: JS
tag: [객체확장표현식]
---

1. # 객체확장 표현식?
   이전 자바스크립트 문법에서 객체를 선언하는데 있어 불편했던 점을 ES6에서 개선했습니다. 객체를 선언하는데 확장된 표현식은 다음과 같습니다.
1. ## 개선된 프로퍼티 이름
   임의의 계산식의 *결과 값을 프로퍼티 이름*으로 사용할 수 있습니다.
   ```javascript
      const prop = "name", i=1;
      const obj = { [prop+i]: "Tom"}; //prop+i의 결과값을 키값으로 지정
   ```
1. ## 프로퍼티 정의의 약식 표기
   프로퍼티 이름이 변수 이름과 같을 때 하나로 줄여서 표현할 수 있습니다.
   ```javascript
      const prop = 2;
      const obj = {prop} //객체이름을 변수이름과 같이 prop으로 설정. {prop:2}와 같습니다.
   ```
1. ## 메소드 정의의 약식 표기
   객체의 프로퍼티 값으로 함수를 지정할 때 function을 생략하고 다음과 같이 나타낼 수 있습니다.
   ```javascript
      const person = { 
         name: "Tom",
         skill: function(){ //밑에처럼 나타낼 수 있습니다.
            console.log('java, c, c#');
         }
      }

      const person2={
         name: "Tom",
         skill(){ //: function을 생략하고 나타낼 수 있습니다.
            console.log('java, c, c#');
         }
      }
   ```
