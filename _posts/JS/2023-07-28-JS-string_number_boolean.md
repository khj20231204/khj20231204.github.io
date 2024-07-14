---
layout: single
title: String, Number, Boolean
categories: JS
tag: []
---

1. # 자동형변환
   ```js
      console.log("90"+10); //9010
      console.log("90"+"10"); //9010

      console.log("90"-10); //80
      console.log("90"-"10"); //80

      console.log("90"*2); //180
      console.log("90"*"2"); //180

      console.log("90"/2); //45
      console.log("90"/"2"); //45
   ```

   "+" 연산자만 문자끼리 합쳐주는 역할을 하고 나머지 "-, *, /" 연산자는 문자라도 산술연산을 수행합니다.   

1. # 명시적 형변환 Stirng, Number, Boolean

   String은 문자형으로 변환   
   Number은 숫자형으로 변환   
   Boolean은 boolean형으로 변환
   하는 함수들입니다.   

   ```js
      console.log(String("12")); //12
      console.log(String('12')); //12
      console.log(String('ab')); //ab
      console.log(String("ab")); //ab
      console.log(String('0')); //0
      console.log(String(0)); //0
      console.log(String(15)); //15
      console.log(String('')); //빈칸출력
      console.log(String(' ')); //빈칸출력
      console.log(String(true)); //true
      console.log(String(false)); //false
      console.log(String(null)); //null
      console.log(String(undefined)); //undefined

      console.log("\n");

      console.log(Number("12")); //12
      console.log(Number('12')); //12
      console.log(Number('ab')); //NaN
      console.log(Number("ab")); //NaN
      console.log(Number('0')); //0
      console.log(Number(0)); //0
      console.log(Number(15)); //15
      console.log(Number('')); //0
      console.log(Number(' ')); //0
      console.log(Number(true)); //1
      console.log(Number(false)); //0
      console.log(Number(null)); //0
      console.log(Number(undefined)); //NaN

      console.log("\n");

      console.log("1 Boolean : " + Boolean("aaa")) //true
      console.log("1 Boolean : " + Boolean(24)) //true
      console.log("1 Boolean : " + Boolean(0)) //false
      console.log("2 Boolean : " + Boolean(NaN)) //false
      console.log("3 Boolean : " + Boolean("")) //false
      console.log("4 Boolean : " + Boolean('')); //false
      console.log("5 Boolean : " + Boolean(" ")) //true
      console.log("6 Boolean : " + Boolean(' ')); //true
      console.log("7 Boolean : " + Boolean( )); //false
      console.log("8 Boolean : " + Boolean(null)) //false
      console.log("9 Boolean : " + Boolean(undefined)) //false
      
      console.log("\n");

      let a1 = 5;
      let a2 = "5";
      console.log(a1 == a2); //true, == 값 비교
      console.log(a1 === a2); //false, === 타입까지 비교
   ```   
   Boolean("aaa") //true   
   Boolean(" ") //true   
   Boolean("") //false   
   문자열과 공백은 true, 빈문자는 false입니다.   
   
