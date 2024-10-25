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

1. # useState사용시 구조분해 할당

   1. 배열 구조 분해 할당   
   ```javascript
      import { useState } from 'react';

      function MyComponent() {
         const [count, setCount] = useState([0, '초기값']);

         // 배열의 첫 번째 요소를 count에, 두 번째 요소를 initialValue에 할당
         const [count, initialValue] = count;

         return (
            <div>
               <p>카운트: {count}</p>
               <p>초기값: {initialValue}</p>
            </div>
         );
      }
   ```
   🔹인덱스 활용: 배열의 각 요소는 인덱스로 접근하기 때문에, 구조 분해 할당 시에도 인덱스 순서대로 변수에 할당합니다.   

   1. 객체 구조 분해 할당   
   ```javascript
      import { useState } from 'react';

      function MyComponent() {
         const [user, setUser] = useState({ name: '홍길동', age: 30 });

         // 객체의 name 프로퍼티를 userName에, age 프로퍼티를 userAge에 할당
         const { name: userName, age: userAge } = user;

         return (
            <div>
               <p>이름: {userName}</p>
               <p>나이: {userAge}</p>
            </div>
         );
      }
   ```  
   🔹프로퍼티 이름 활용: 객체의 프로퍼티 이름을 사용하여 값을 추출합니다.   
   🔸별칭 사용: name: userName과 같이 별칭을 사용하여 다른 이름으로 변수에 할당할 수 있습니다.   
   🔺기본값 설정: 프로퍼티가 존재하지 않을 경우 기본값을 설정할 수 있습니다.   
      예) const { name = '익명', age } = user;   

