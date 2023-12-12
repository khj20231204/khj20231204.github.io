---
layout: single
title: ==와 equals
categories: JAVA
tag: [equals]
---

1. # "=="    
   int,float,long,double 와 같은 primitive 타입에서 "=="의 사용법과 클래스, 배열과 같은 refrece타입에서 "==" 사용법은 다릅니다.
1. # primitive타입 사이에서의 "==" 사용
   두 변수의 __값__ 이 같은지 비교합니다.
   ```java
      int num1 = 9;
      int num2 = 9;
      System.out.println(num == num2); //true
   ```
1. # refrece타입 사이에서의 "==" 사용
   두 객체의 __주소__ 가 같은지 비교합니다. 두 객체의 메모리 주소를 비교합니다. 객체의 내용이 같은지 비교한는 것이 아니라 객체가 가리키는 주소값을 비교하여 동일성 체크를 합니다
   ```java
      String str1 = new String("hello"); //String클래스로 인스턴스 생성
      String str2 = new String("hello");
      System.out.println(str1 == str2); // false
   ```
   str1과 str2는 "hello"로 같은 문자열이지만 각각 new 연산자로 새로운 인스턴스를 생성했기 때문에 주소값이 다릅니다
1. # String 클래스에서 "==" 사용
   ```java
      String str1 = "hello"; //"hello"라는 문자열 리터럴 주소값이 str1에 저장
      String str2 = "hello"; 
      System.out.println(str1 == str2); //true
   ```
   "str1==str2"는 값이 같아서 true가 나온 것이 아니라 str1과 str2가 모두 같은 "hello"라는 __문자열 리터럴 주소값을 할당__ 받았기 때문입니다. 즉 str1과 str2가 가리키는 주소값이 같아서 true가 나온 것입니다.
1. # equals
   equals메서드는 모든 자바 클래스의 최상위 클래스인 Object클래스에 포함되어있는 메서드입니다. 기본적인 equals메서드는 "=="와 똑같은 동작 방식으로 메모리 주소를 비교하여 같은 객체인지를 판단합니다. 하지만 상당부분의 클래스에서 equals를 값을 비교하기 위한 메서드로 오버라이딩해서 사용합니다. 대표적인 클래스가 String입니다. String에서는 equals가 값을 비교하기 위한 메서드로 작동합니다.
   ```java
      String str1 = new String("hello"); //String클래스로 인스턴스 생성
      String str2 = new String("hello");
      System.out.println(str1 == str2); // false
      System.out.println(str1.equals(str2)); // true
   ```
   str1과 str2가 new연산자로 각각 다른 메모리 공간을 할당 받았고 그 주소값이 str1과 str2에 입력되었기 때문에 주소값을 비교는하는 "==" 연산의 결과는 false가 되고 재정의되어 값을 비교하는 equls는 "hello"로 값이 같기 때문에 true를 반환합니다.   
1. # 정리
   == : primitivm 값 비교, reference 주소 비교   
   equals : 기본값은 주소 비교, String 값 비교   
   *문자열 리터럴은 주소값을 반환