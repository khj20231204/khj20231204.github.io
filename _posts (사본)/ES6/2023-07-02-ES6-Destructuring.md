---
layout: single
title: Destructuring Assignment(비구조화 할당)
categories: ES6
tag: [배열 리터럴, 객체 리터럴, 이터러블]
---

1. # 비구조화 할당이란?
   배열, 객체, 반복가능 객체에서 값을 꺼내 별도의 변수(배열 리터럴 변수, 객체 리터럴 변수)에 개별적으로 할당하는 것을 말합니다. 
   배열과 같은 이터러블 또는 객체 리터럴에서 필요한 값만 추출하여 변수에 할당할 때 사용됩니다.
1. # 이터러블하다?
   배열, 문자열 등을 사용할 때 필요한 값에 접근하기 위해서 for문, for..in문, forEach메소드 등을 이용해서 순회하며 원하는 값을 가져옵니다.
   자바의 Collection Framwork의 컬렉션 요소에 접근할 때 데이터는 컬렉션에 저장하고 각 요소에 접근하는 기능을 가진 Iterator(반복자)인터페이스를 정의하여
   이를 상속받아 구현해 컬렉션의 데이터를 가지고 오듯이 순회 가능한 데이터 컬렉션을 접근하는데는 동일한 방법이 쓰입니다. ES6부터 이를 프로토콜로 정의하여 
   이를 이터레이션 프로토콜이라 합니다. 이터레이션 프로토콜에는 이터러블 프로토콜과 이터레이터 프로토콜이 있는데 이터러블 프로토콜을 준수한 객체를 이터러블이라 합니다.
   간단히 lterator(반복자)를 직접 구현한 메소드가 있거나 객체를 상속 받았으면 '이터러블하다'라 하고합니다.
1. # 배열 비구조화 할당
   배열에 있는 요소의 값들을 배열 리터럴 변수에 각각 할당하여 따로 조작이 가능합니다. 할당 기준은 배열의 인덱스입니다.
   ```javascript
      /* 우측 배열을 좌측 변수에 담아서 a,b,c,rest로 각각 접근하는 것이 목적 */
      [a,b,c] = [5,8]; //a=5, b=8, c=undefined
      [a,b] = [4,9,2]; //a=4, b=9
      [a,b, ...rest] = [32,56,56,75,22] //a=32, b=56, rest=(3)[56,75,22]
   ```
1. # 객체 비구조화 할당
   할당 기준이 프로퍼티 키이기 때문에 순서는 의미가 없으며 선언된 객체 리터럴 변수 이름과 프로퍼티 이름이 일치해야 합니다.
   ```javascript
       const data = {
         first: 'south',
         second: 'korea'
      }
      const {second, first} = data;
      console.log({second}, second); //{second: 'korea'} 'korea'
      console.log({first}, first); //{first: 'south'} 'south'
   ``` 
   객체의 순서는 상관없이 프로퍼티의 이름과 일치하는 변수에 저장됩니다.   
   {first}를 사용하면 프로퍼티 전체를 불러오고 first를 사용하면 프로퍼티 값만 불러옵니다
1. # 함수로 전달할 때
   ```javascript
      <script>
      const obj = {
        user: {
         name: "kim",
         age: 10
        },
        color: "red",
        children: '<div>hello</div>'
      };

      function part1({user}) { //obj객체의 user프로퍼티를 할당 
          console.log({user}); //user: {name: 'kim', age: 10}
          console.log(user) //{name: 'kim', age: 10} age: 10 name: "kim"
          console.log(user.name); //kim
          console.log(user.age); //10
      }
      
      function part2({color}) { //obj객체의 color프로퍼티를 할당
          console.log({color}); //{color: 'red'}
          console.log(color); //red
      }
      function part3({children}) { //obj객체의 children프로퍼티를 할당
          console.log({children}); //{children: '<div>hello</div>'}
          console.log(children); //<div>hello</div>
      }

      function all(props) { //obj전체를 할당, props = obj 와 같음
          console.log(props); //{user: {…}, color: 'red', children: '<div>hello</div>'}
      }

      part1(obj); 
      part2(obj); 
      part3(obj); 
      all(obj);
   </script>
   ```
   ● 값 할당 시   
   객체를 쪼개서 변수로 사용하고 싶을 때 { }이용.
   ● 사용 시
   {a}에서 { }를 사용하면 전체 프로퍼티를, a를 사용하면 값만 사용

