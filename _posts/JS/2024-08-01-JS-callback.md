---
layout: single
title: bacllback
categories: JS
tag: []
---
 
1. # callback
   다른 함수의 매개변수로 전달되는 함수를 의미합니다. 즉, 함수를 데이터처럼 취급하여 다른 함수에게 넘겨주는 것이죠. 이렇게 전달된 함수는 특정 조건이나 이벤트가 발생했을 때 호출되어 원하는 작업을 수행하도록 설계됩니다.   
  
   제어권 위임: 자신을 제어할 수 있는 권한을 다른 객체에 넘기는 것을 말합니다.   
   
   제어권한의 종류   
   1)실행시점   
   2)매개변수   
   3)this   

   1)실행시점 위임
   ```js
      setInterval(function(){
         console.log('1초마다 실행');
      }, 1000);
   ```   
   setTimeout도 실행시점에 대한 제어권을 넘겨주는데요. setInterval도 마찬가지입니다.

   ```
      setInterval(callback, milliseconds);
   ```   
   setInterval에 callback함수를 넘겨주면 setInterval이 알아서 milliseconds의 시간마다 callback함수를 실행시켜줍니다. 즉, callback함수의 제어권을 setInterval함수에 넘겨주는 것입니다.   

   2)매개변수 위임
   ```js
      var arr2 = [1,2,3,4];
      var entries = [];
      arr2.forEach(function(v,i,a){
         entries.push(v,i,this[i])
      },[10,20,30,40]);
      console.log(entries); 
      
      결과값:
      [1, 0, 10, 2, 1, 20, 3, 2, 30, 4, 3, 40]
   ```   
   forEach(function(v,i,a))에서 v,i,a의 순서가 매개변수의 위임이 됩니다. 순서를 임의대로 변경할 수 없기 때문입니다.   

   3)this 위임
   ```
      
   ```

1. # 

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
