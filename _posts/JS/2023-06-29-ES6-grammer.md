---
layout: single
title: grammer
categories: JS
tag: [배열,객체,프로퍼티]
---

1. # Shorthand property names
   새로운 객체를 변수에서 값을 가져와서 간단하게 선언 가능합니다. 단 변수명이 객체 프로퍼티의 이름이 됩니다.
   ```javascript
      const username="kitty";
      const age = 21;
      const student = {username, age}; //변수를 student에 할당
      console.log(student); //{username: 'kitty', age: 21}
   ```
1. # Spread Operator(전개 연산자)   
   배열이나 객체를 전개할 때 ...(점 3개)로 나타냅니다. 함수 호출 및 선언, 배열 선언, 객체 선언시 다양하게 활용할 수 있습니다.   
   <h6>1)함수 선언 시 SpreadSyntax는 <span style="color:red">마지막 파라미터에 한해</span> 사용할 수 있습니다.</h6>
   <h6>2)배열 선언 시 같은 값들이 있어도 계속 추가 됩니다</h6>
   <h6>3)객체 선언 시 같은 이름이 있으면 가장 마지막에 값들이 저장됩니다.</h6>
   ```javascript   
      //1)함수 인수로 활용
      function sum(x,y,z){
         return x+y+z;
      }
      const arr = [3,5,6];
      const s = sum(...arr); //함수 인수로 활용
      console.log(s)

      //2)함수 선언 시 활용
      function func(name, age, ...adv){ //마지막 인자로만 활용
         console.log(`${name}는 ${age}살 이고 특기는 ${adv}입니다`);
      }
      func("kitty","2","밥먹기, 책보기, 영화보기"); //kitty는 23살 이고 특기는 밥먹기, 책보기, 영화보기입니다

      //3)배열 선언 시 활용
      const a = [1,2,3];
      const b = [2,3,9];
      const c = [...a,...b];
      console.log(c) //[1, 2, 3, 2, 3, 9] a의 2,3과 b의 2,3 모두 추가

      //4)객체 선언 시 활용
      const student = {
         name: "kitty",
         age: 24
      }
      const person = {...student, age:69, height:152, weight: 80}
      console.log(person); //{name: 'kitty', age: 69, height: 152, weight: 80}
   ```   
1. # 연산자||   
      <h3>비교값A || 비교값B → 비교값을 반환</h3>
      비교값A가 true이면 비교값A를 반환하고, false이면 비교값B를 반환합니다.   
      false인 경우: 배열에서 없는 값, 0, -0, NaN, null, false, undefined, 빈문자열은 false를 반환합니다.   
      ```javascript
         var arry = ['one','two']
         var chk = arry[3] || 'empty'; //empty
         var chk = 0 || 2; //2
         var chk = NaN || 2; //2
         var chk = "" || 2; //2
         var chk = false || 2; //2
         var chk = null || 2; //2
      ```
      <h3>조건A || 조건B</h3>   
      조건A와 조건B 중 하나만 true이면 true를 반환, 둘 다 false이면 false를 반환합니다.   

