---
layout: single
title: Promise와 async
categories: REACT
tab: 
---

1. # 비동기를 사용하는 이유
   동기(Synchronous) : 기다림   
   비동기(Asynchronouse) : 안기다림   

   웹 애플리케이션에서 API로 서버 측에 데이터를 요청할 때 클라이언트 쪽의 cpu 처리속도와 네트워크를 타고 데이터를 받아오는 API처리 시간은 당연히 delay가 발생할 수 밖에 없습니다. CPU속도는 GHz단위의 주파수로 처리가 되고 네트워크는 Mbps의 데이터 전송량으로 처리가 됩니다. GHz는 1초당 클럭 사이클 횟수를 의미하는데 3GHz란 1초에 30억 번의 클럭 사이클을 수행한다는 의미입니다. 클럭 사이클이 높을수록 CPU는 더 많은 명령어를 처리할 수 있습니다. Intel Core i7 2.9GHz인 경우 1초에 29억 번의 명령어를 처리할 수 있다는 의미가 됩니다. 반면, 네트워크의 Mbps는 1초당 100만 비트의 데이터를 전송할 수 있다는 의미입니다. 50Mbps인 경우 1초당 5000만 비트를 전송하게 됩니다. 네트워크 환경은 렉이나 collision 같은 딜레이가 발생할 수 있고, 물리적 거리, 네트워크 장비 장애, 패킷 손실 등 여러가지 이유로 인해 지연이 발생할 수 있습니다. 게다가 CPU는 캐쉬 메모리를 사용하고 서버의 데이터는 하드웨어 메모리에 저장되어 있습니다. 인간의 관점이 아니라 컴퓨터이 관점으로 CPU와 API의 데이터 처리 속도를 비교하면 상당히 많은 차이가 발생한다는 것을 알 수 있습니다. 이러한 지연을 방지하기 위해 비동기 방식의 처리를 하게됩니다. 기본적 인터프리터 방식인 자바스크립트의 경우 위에서부터 차례대로 실행을 하게 되는데 동기방식의 경우 서버쪽으로 데이터를 요청 후 응답이 올 때까지 기다려야하지만 비동기방식은 다음 행으로 넘어가서 코드를 실행하게 됩니다.  

1. # 콜백함수
   매개변수로 받은 함수를 처리가 끝난 후 함수 안에서 매개변수를 받은 함수를 다시 호출할 경우 이 함수를 __콜백 함수__ 라고 합니다.   

   ```javascript
       function increase(number, cb){ //cb이름으로 함수를 매개변수로 전달
         console.log("----- 1 -----")
         setTimeout(() => {
            console.log("----- 2 -----")
            let result = number + 10; //매개변수 number에 10을 더해서 result를 만듦
            if(cb) { //매개변수 db가 false가 아니면.. 
               console.log("----- 3 -----")
               cb(result); //콜백함수(매개변수로 받은 함수)에 result 대입, cb로 받은 함수 호출
               console.log("----- 4 -----")
            }
         }, 3000)
      }

   increase(0,(r)=>{console.log(`mycall function (result : ${r})`)}) 
   //처음에 호출만 하고 (r)=>{ }이 실행되지는 않음. 이후 콜백으로 결과 값으로 받을 때 (r)=>{ }이 실행

   - 실행 결과 -    
   ----- 1 -----  
   ----- 2 -----   
   ----- 3 -----   
   mycall function (result : 10)   
   ----- 4 -----   
   ```

1. # 콜백함수 중첩
   결과 값을 10, 20, 30 이렇게 나타내고 싶다면 콜백함수를 중첩할 수 있습니다.   

   ```javascript
      function increase(number, cb){ //cb이름으로 함수를 매개변수로 전달
         console.log("----- 1 -----")

         setTimeout(() => {
            console.log("----- 2 -----")
            let result = number + 10; //매개변수 number에 10을 더해서 result를 만듦
            if(cb) { //매개변수 db가 false가 아니면.. 
               console.log("----- 3 -----")
               cb(result); //콜백함수(매개변수로 받은 함수)에 result 대입, cb로 받은 함수 호출
               console.log("----- 4 -----")
            }
         }, 3000)
      }

      increase(0,(r)=>{
      console.log(`mycall function (result : ${r})`)
         increase(r, r=>{
            console.log(`mycall function (result : ${r})`)
            increase(r, r=> { 
               console.log(`mycall function (result : ${r})`)
            })
         })
      })

      - 실행 결과 -
      ----- 1 -----
      ----- 2 -----
      ----- 3 -----
      mycall function (result : 10)
      ----- 1 -----
      ----- 4 -----
      ----- 2 -----
      ----- 3 -----
      mycall function (result : 20)
      ----- 1 -----
      ----- 4 -----
      ----- 2 -----
      ----- 3 -----
      mycall function (result : 30)
      ----- 4 -----
   ```

1. # Promise
   위와 같이 콜백 함수를 계속 호출하여 원하는 결과를 얻어야 하는 경우 중첩을 하게되고, 그 결과 가독성과 이해가 어려워지게 됩니다. 이를 방지하기 위해 ES6부터 도입된 promise라는 기능이 있습니다. 함수를 여러번 호출하는 대신 then이란 명령어를 덧붙입니다. 가독성만 약간 높이는 기능입니다.   

   Promise 객체의 .then 메서드 : 이전 Promise가 resolve될 때 실행될 함수를 등록하는 역할을 합니다.   
   increase 함수의 작업이 완료되어 'return promise'가 호출될 때 r1에 등록된 then의 함수가 실행됩니다.   

   ```javascript
      const PromiseFunc = () => {

      let increase = (number) => {

         console.log("---- 2 ----")

         let promise = new Promise((r1, reject) => { //Promise 선언
            
            console.log("---- 3 ----")

            setTimeout(() => {
               console.log("---- 4 ----")
               let r = number + 10;
               if(r > 50){
                  return reject("reject in error");
               }
               console.log("---- 5 ----")
               r1(r);   //Promise의 함수 r1의 매개변수로 r 전달 .then부분의 함수가 매개변수로 r을 받으면서 실행
               console.log("---- 6 ----")
            }, 1000);
         })

         return promise;
      }

      increase(0) 
      .then(number => {  //increase가 완료되어 "return promise"가 될 때 r1으로 then에 등록된 함수가 실행
         console.log("1 : " +number);
         return increase(number)
      })
      .then(number => {
         console.log("2 : " + number);
         return increase(number);
      })
      .catch( e => {
         console.log(e)
      })

      - 실행 결과 -
      ---- 2 ----
      ---- 3 ---- //1초후 밑에 4실행
      ---- 4 ----
      ---- 5 ----
      ---- 6 ----
      1 : 10
      ---- 2 ----
      ---- 3 ----
      ---- 4 ----
      ---- 5 ----
      ---- 6 ----
      2 : 20
      ---- 2 ----
      ---- 3 ----
      ---- 4 ----
      ---- 5 ----
      ---- 6 ----
   ```