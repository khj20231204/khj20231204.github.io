---
layout: single
title: (obj)와 ({obj})
categories: REACT
tab: 
---

1. # (obj)와 ({obj})
   ```javascript
      const obj = { name: 'Alice', age: 30 };

      console.log(obj); // 출력: { name: 'Alice', age: 30 }
      console.log({obj}); // 출력: { obj: { name: 'Alice', age: 30 } }
   ```   
   console.log(obj);   
   직접 출력: props 객체 자체를 그대로 콘솔에 출력합니다.   

   console.log({obj});   
   객체 안에 객체 포함: props 객체를 또 다른 객체 안에 넣어서 출력합니다. 즉, { props: props }와 같은 형태입니다.   

   console.log(props);는 props 객체의 내용을 바로 보여줍니다.   
   console.log({props});는 props 객체를 하나의 속성으로 감싸서 더 구조적인 형태로 보여줍니다.   