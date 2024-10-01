---
layout: single
title: 함수 실행
categories: REACT(Lesson)
tag: []
author_profile: false
---

1. # jsx { }에서 함수 실행
   ```java
      let getAddResult = () => {
         let sum = 10;
         console.log("sum:"+sum);
         return sum; //getAddResult()으로 실행시 return
      };

      function App() {
         return <div>
            합계 : {getAddResult}  //error 발생

            합계 : {getAddResult()} //getAddResult의 함수를 실행, return 값을 받아옴
            </div>
      }
   ```   
   {getAddResult} : error 발생   
   getAddResult란 함수의 주소값을 바인딩 시키게 되는데 주소값을 문자열로 출력하려고 하기 때문에 에러발생   

   {getAddResult()} : getAddResult란 함수를 실행하면서 결과 값을 받아옵니다.   
   콘솔 - sum:10   
   html페이지 - 합계 2 : 10   

   jsx안에서 { } 안에 함수를 사용할 때는 __( ) 사용__   


1. # 이벤트로 함수 실행
   ```javascript
      let number = 1;

      const add = () => {
         number++;
         console.log(number);
         return number;
      }

      function App() {
         return (
            <div>
               <h1>숫자 : {number}</h1>
               <button onClick={add}>더하기</button> 
               <button onClick={add()}>더하기</button> //error 발생
         )}
   ```
   onClick으로 함수를 바인딩 시킬 때는 add 함수의 주소값을 참조 시켜야합니다.   
   add()은 add함수를 실행 후 리턴값을 반환하기 때문에 onClick에 바인딩 시킬 수가 없어서 에러가 발생합니다.   

   이벤트에서 함수를 사용할 때는 __( ) 생략__
   