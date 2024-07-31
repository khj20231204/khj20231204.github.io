---
layout: single
title: call/apply/bind
categories: JS
tag: []
---
 
1. # call
   call 함수는 자바스크립트에서 함수의 this 값을 임의로 바꿔 호출할 수 있도록 해주는 강력한 도구입니다. 즉, 어떤 함수를 호출할 때, 그 함수 내에서 this 키워드가 가리키는 객체를 우리가 원하는 객체로 바꿔서 사용할 수 있게 해줍니다.   

   ```
      call : func.call(thisArg[, arg1[, arg2[, ...]]])   
   ```   
   
   ```js
      let part1 = {
      name : "part1"
     }

     let part2 = {
      name : "part2"
     }

     function exCall(x){
         console.log(`${x} ${this.name}`)
     }
      
     exCall.call(part1, "a"); //a part1
     exCall.call(part2, "b"); //b part2
     exCall("c");             //c
   ```   

1. # apply
   call과 유사한 기능을 제공하지만 매개변수로 배열받는다는 점이 call과 다릅니다.   
   
   ```
      apply : func.apply(thisArg, [argsArray]);
   ```   

   ```js
      let arr1 = [3,6,7,1,4];

      console.log(Math.max(...arr1));         //7
      console.log(Math.max.apply(null, arr1));//7
   ```   

1. # bind

   |     특징    |      call     |        bind       |
   |:-----------:|:--------------:|:----------------:|
   |  함수 실행  |     즉시 실행   |  새로운 함수 생성  |
   | this값 설정 |   호출 시 설정  |  생성시 설정      |
   | 인수 전달   | 개별적으로 전달 | 일부 인수 고정 가능 |

   언제 어떤 메서드를 사용해야 하나?   
   __call:__ 함수를 바로 실행하고, this 값을 유연하게 변경해야 할 때 사용합니다. 예를 들어, 다른 객체의 메서드를 빌려 사용하거나, 함수의 실행 컨텍스트를 변경하고 싶을 때 유용합니다.   
   __bind:__ 함수를 미리 설정하여 나중에 호출하고 싶거나, 특정 인수를 고정하여 재사용 가능한 함수를 만들고 싶을 때 사용합니다. 이벤트 핸들러, setTimeout, setInterval 등과 함께 자주 사용됩니다.    

   인수 고정
   ```js
      function multiplier(a,b){
      return a * b;
     }

     let result1 = multiplier.bind(null, 2); //인수 고정
     let result2 = result1(5);
     console.log(result2); //10
   ```   
   
   bind는 새로운 함수를 생성시 this값이 설정되기 때문에 참조 변수를 할당하여 __변수로 호출__ 해야 합니다.  

   변수로 호출하여 실행
   ```js
      let obj1 = {
      name : "obj1"
     }

     let obj2 = {
      name : "obj2",
      f : function(){
         console.log(`this : ${this.name}`);
      }
     }

     obj2.f(); //this : obj2

     let callFunc = obj2.f.bind(obj1) //변수에 할당
     callFunc();  //변수로 호출, this : obj1
   ```