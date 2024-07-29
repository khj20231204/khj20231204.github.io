---
layout: single
title: 변수 선언
categories: JS
tag: [변수, 초기화, 스코프]
---

1. # 변수란?
   변수 선언이란 변수 이름과 확보된 메모리 공간의 주소를 연결해서 값을 저장할 수 있게 준비하는 것입니다.
1. # 실행 단계   
   ◆ 소스코드 평가 단계 : 소스코드 실행을 위한 준비 단계로 변수 선언, 함수 선언, 배열 선언등 모든 선언문을 소스코드에서 찾아 먼저 실행합니다.    
   ◆ 소스코드 실행 단계 : 런타임 단계라고도 하며 인터프리터에 의해 선언문을 제외한 소스코드가 순차적으로 실행됩니다.   
1. # 변수 선언 단계   
   자바스크립트 엔진 변수 선언 단계입니다.
   ◆ 변수 선언 단계 : *소스코드 평가 단계*에서 수행되며 변수 이름을 메모리에 등록해서 자바스크립트 엔진에 변수의 존재를 알립니다.     
   ◆ 초기화 단계 : 값을 저장하기 위한 메모리 공간을 확보하고 암묵적으로 undefined를 할당해 초기화합니다.   
   ◆ 값 할당 단계 : *런타임 단계*에서 수행되며 '='연산자를 통해 변수의 새로운 메모리 공간에 값을 저장합니다.   
1. # var키워드   
   var키워드로 선언한 경우는 선언 단계와 초기화 단계가 동시에 진행됩니다. 소스코드 평가 단계에서 선언를 통해 변수 이름을 등록하고, 바로 암묵적으로 undefined를 할당해 초기화 합니다. 변수의 중복 선언 허용. 오로지 함수의 코드 블록만 지역 스코프로 인정합니다.
   ```javascript
      var a = 10;
      var a = 15; //중복 선언 허용

      var b = 5;
      function func1(){
         var b = 10
         console.log("func1 start:"+b) //10 함수 내에서만 b=10 : 함수레벨 스코프
         if(true){
          b = 9;
          console.log("if문:"+b) //if문:9
         }
         console.log("func1 end:"+b) //func1 end:9 조건문이 끝나도 계속9
      }
      func1();
      console.log("fun1c 밖:"+b) //fun1c 밖:5 
   ```
1. # let키워드
   블록 레벨 스코프를 따른다. 모든 코드 블록(함수, if문, for문, while문, try/catch문 등)을 지역 스코프로 인정한다. 중복 선언 금지.
   ```javascript
      let l = 3;
      //let l = 6; error발생

      function func2(){
      let l = 5;
      console.log("func2 start:"+l) //func2 start:5
      if(true){
        let l = 9;
        console.log("if문:"+l) //if문:9
      }
      console.log("func2 end:"+l) //func2 end:5 조건문이 끝면 다시5
      }
      func2();
      console.log("func 밖:"+l) //func 밖:3
   ```
1. # const키워드
   let로 선언한 변수와 동일하게 동작하지만 다음 두가지에서 다릅니다.   
   1)반드시 초기화해야 합니다.   
   2)한번 선언한 변수는 수정이 불가합니다.   
   단. 선언한 상수 값이 객체이거나 배열인 경우 변경가능합니다.   
   ```javascript
      const a; //error발생
      const a=3;
      a=5; //error발생
      const obj = {x:1, y:2};
      obj.x = 4;
      console.log(obj.x) //4

      const arr = [1,2,3,4];
      arr[1] = 5;
      console.log(arr); //[1,5,3,4]
   ```