---
layout: single
title: 하루하루
categories: CODINGTEST
tag: [wapper, primitive]
---

1. # char ch=ch-32 와 char ch-=32; 차이
   ```java
      char ch1 = 'a'; 
      //ch1 = ch1-32; error발생 -- ㉠
        
      char ch2 = 'a'; 
      ch2 -= 32; //가능 -- ㉡
   ```
   ㉠이 error인 이유는 ch1-32의 결과가 int형인데 이 int형을 char형에 넣었기 때문이다. 강제형변환을 하면 error발생은 나지 않는다.   
   ch1 = (char)(ch1-32);   
   ㉡이 error가 발생하지 않는 이유는 컴파일러가 -= 와 += 의 경우 자체 형변환을 하기 때문이다.
   
1. # List값 가져오기
   ```java
   List<Car> list  = new ArrayList();
   for(Car c : list){ // -- ㉠
      System.out.println(c.price);
   }
   ```
   ㉠ List의 제네릭 타입형을 for(foreach : x)문에서 받는다   
