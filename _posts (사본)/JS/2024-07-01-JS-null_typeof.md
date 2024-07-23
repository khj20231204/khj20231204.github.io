---
layout: single
title: 따옴표, null, typeof
categories: JS
tag: []
---
 
1. # 따옴표
   문자열 표현은 `"` , `'`, \` 3가지 입니다.

   ```js
      const name1 = "Mike";
      const name2 =  'Mike';
      const name3 = `Mike`;

      const name4 = "I'm";
      const name5 - 'I\'m';
   ```   
      `" "`와 `' '` 는 차이가 없음.   
      `'` 앞에 `\`를 사용하면 `'` 사용가능   

   ```js
      const name2 = `My name is ${name1}`;
      const age = 30;
      const name3 = `My age is ${age + 5}`; //My age is 35
   ```   
   \` \` 안에 `${}` 를 사용하면 변수 출력 가능   

1. # NaN
   Not a Number

   ```js
      console.log('b'/5); //NaN
   ```   

1. # null 과 undefined
   null : 선언하지 않음(존재하지 않음)   
   undefined : 선언은 했지만 값을 할당 받지 않음   

1. # typeof
   ```js
      console.log(typeof 3); //number
      console.log(typeof msg); //string
      console.log(typeof true); //boolean
      console.log(typeof "xxx"); //string
      console.log(typeof null);  //object
      console.log(typeof undefined); //undefined
   ```   
   null의 typeof가 object가 나오는데 이것은 예전 버젼과의 호환성 때문에 놔둔 것이지 null은 object가 아닙니다.   
