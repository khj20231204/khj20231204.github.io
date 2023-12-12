---
layout: single
title: 화살표 함수
categories: ES6
tag: [화살표함수]
---

1. ## 화살표 함수 작성법
   1. ### 일반적 표현
   ```javascript
      var f = function(x) {return x*x;}
   ```
   1. ### 인수가 여러 개 
   ```javascript
      var f = (x,y,z) => {return x+y+z;}
   ```
   1. ### 인수가 하나 : 인수를 묶는 괄호{} 생략 가능
     ```javascript
      var f = x => {return x}
   ```
   1. ### 인수가 없는 경우 : 묶는 괄호{} 생략 불가
   ```javascript
      var f = () => {return y;}
   ```
   1. ### body에 return문만 있는 경우 : return 키워드 생략 가능
   ```javascript
      var f = x => x*x;
   ```              
   1. ### body에 return문만 있는 경우 : 반환값이 객체이면 ()로 묶습니다.
   ```javascript
      var f = (a,b) => ({x:a, y:b});
   ```
1. ## 함수 리터럴과 화살표 함수의 차이


