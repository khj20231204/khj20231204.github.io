---
layout: single
title: 구조분해 할당
categories: REACT
tab: 
---

1. # 정의
   구조 분해 할당은 배열이나 객체의 요소 또는 속성을 분해하여 각각의 변수에 할당하는 기능입니다.   

1. # 예시

   __배열열 구조 분해 할당__   
   ```javascript
      const numbers = [1, 2, 3];
      const [first, second] = numbers;

      console.log(first); // 1
      console.log(second); // 2
   ```
   <br>
   __객체 구조 분해 할당__
   ```javascript
      JavaScript
      const person = { name: '홍길동', age: 30 };
      const { name, age } = person;
      //const { name } = person; 도 가능
      //const { age } = person; 도 가능

      console.log(name); // 홍길동
      console.log(age);   // 30
   ```
   <br>
   __함수의 매개변수__   
   ```javascript
      function printUser({ name, age }) {
         console.log(`이름: ${name}, 나이: ${age}`);
      }

      const user = { name: '김철수', age: 25 };
      printUser(user);
   ```

