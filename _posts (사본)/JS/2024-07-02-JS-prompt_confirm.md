---
layout: single
title: prompt, confirm, 연산자
categories: JS
tag: []
---
 
1. # prompt
   ```js
      const age = prompt("나이를 입력하세용","18");
      console.log(age);      
   ```   
   prompt(a) 또는 prompt(a,b)를 입력받는데 매개변수가 1개인 경우 a의 메세지를 출력하고 2개인 경우 a의 메세지를 출력하고 입력란에 기본 값으로 b가 출력됩니다.   

   age값으로 입력받은 값이 출력됩니다.   

1. # confirm
   ```js
      const isAdult = confirm("성인 입니깡?");
      console.log(isAdult);
   ```   
   prompt는 값을 입력받게 되는데 confirm은 "확인"버튼과 "취소"버튼 2개가 출력되며 따로 입력받지는 않습니다.   
   "확인"을 클릭한 경우 isAdult가 ture를 반환하며 "취소"를 클릭한 경우 isAdult가 false를 반환합니다.   

1. # number
   ```js
      const a = prompt("수학은 몇 점?"); //90입력
      const b = prompt("영어는 몇 점?"); //80입력

      console.log(a+b); //9080
   ```   
   prompt로 입력받은 값은 전부 문자열로 인식하기 때문에 a와 b 2개의 문자를 더한게 됩니다.   

   ```js
      console.log(Number(a)+Number(b)); //170출력
   ```   
   Number 함수를 사용하여 숫자로 바꿔줍니다.   
   *number(x), Number(o)   








