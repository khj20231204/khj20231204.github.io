---
layout: single
title: 헷갈리는 표기
categories: REACT
tab: 
---

```javascript
   <div style={ `{`padding:20, color:'blue' `}` }>{children}</div>
   /*
   HTML안에서 객체 프로퍼티 구분은 ,로 구분.
   padding과 color를 ,로 구분.
   ,대신 ; 사용안됨.
   */

   <MyComponent user={`{` name: "kevin", age: 10 `}`} color='red'/>
   /*
   속성과 속성 사이 , 사용 안함.
   빈 공백으로 구분.
   */
```
