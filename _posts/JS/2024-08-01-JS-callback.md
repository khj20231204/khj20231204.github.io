---
layout: single
title: bacllback
categories: JS
tag: []
---
 
1. # callback
   다른 함수의 매개변수로 전달되는 함수를 의미합니다. 즉, 함수를 데이터처럼 취급하여 다른 함수에게 넘겨주는 것이죠. 이렇게 전달된 함수는 특정 조건이나 이벤트가 발생했을 때 호출되어 원하는 작업을 수행하도록 설계됩니다.   
   자바스크립트에서는 함수를 객체 취급하게 되고, 객체란 데이터가 

   ```js
      var callback = () =>{
         console.dir(this);
      }

      var obj = {
         a : 1,
         b : function(cb){
            cb();
         }
      };

      obj.b(callback);

      결과값:
      Window
      alert : ƒ alert()
      atob : ƒ atob()
      blur : ƒ blur()
      btoa : ƒ btoa()
      ...
   ```   


1. # 함수를 객체로 사용
   1)객체를 값으로 처리
   ```js
      var a = function(){  //function을 변수 a에 할당, 이것 자체가 함수를 값으로 취급한 경경
         ...
      }

      var obj = {
         a : 1,
         b : function(){   //객체의 프로퍼티로 함수를 사용

         }
      }

   ```

   2)함수의 인자로 함수 전달    
   ```js
       function f(f2, n){
         return f2(n);
      }

      function sendA(n){
         return n+1;
      }

      function sendB(n){
         return n+10;
      }

      console.log(f(sendA,10));  //함수sendA를 매개변수로 전달
      console.log(f(sendB,10));  //함수sendB를 매개변수로 전달
   ```   

   3)함수는 함수를 리턴한다   
   ```js
      function fun(mode){
         var obj = {
            'case1' : function(a,b){return a+b;},
            'case2' : function(a,b){return a-b;}
         }

         return obj[mode]; //return obj.mode 오류 발생
         //obj의 case1에 해당하는 함수를 리턴
      }

      console.log(fun('case1')(1,3));
   ```   
   `return obj[mode]`   
   리턴 값으로 함수가 가능하며 return console.log("case1")처럼 콘솔도 리턴이 가능합니다.   

   4)함수는 프로퍼티를 가질 수 있다   
   ```js
      function add(x,y){
         return x+y;
      }

      add.result = add(4,5);
      add.status = 'complete';

      console.log(add.result);
      console.log(add.status);
   ```
