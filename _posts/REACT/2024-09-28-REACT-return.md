---
layout: single
title: 명시적 반환, 암묵적 반환
categories: REACT
tab: [react]
---

1. 암묵적 반환과 명시적 반환

   암묵적 반환   
   ```JavaScript
      let num = state.findIndex((e) => e.id === action.payload);
   ```   
   암묵적 반환: 화살표 함수의 중괄호 {}를 생략하고, 단일 표현식 e.id === action.payload만 작성했습니다. 이 경우, 화살표 함수는 자동으로 이 표현식의 결과를 반환합니다. 즉, e.id가 action.payload와 일치하면 true인 경우 해당 인덱스를 반환합니다.   

   명시적 반환   
   ```javascript
      let num = state.findIndex((e) => { return e.id === action.payload; });
   ```
   명시적 반환: 화살표 함수의 중괄호 {}를 사용하고, return 키워드를 통해 e.id === action.payload의 결과를 명시적으로 반환합니다. 이 경우에도 암묵적 반환과 동일하게 true인 경우 해당 인덱스를 반환합니다.   