---
layout: single
title: 래퍼 클래스
categories: JAVA
tag: 
---

1. # 기본 타입과 래퍼 클래스
   자바는 기본 타입(byte, char, short, int, long, double, float)에 해당하는 각각의 객체를 생성할 수 있습니다. 매개변수로 객체를 요구할 때, 기본형 값이 아닌 객체를 요구할 때, 객체간 비교를 해야할 때 등 객체를 사용해야 할 때가 있는데 주로 컬렉션 프레임 워크에서 기본 타입 값을 객체로 생성해서 관리하게 됩니다.   
   이렇게 기본형(Primitive type)을 객체로 생성할 수 있게 만드는 클래스를 래퍼 클래스(Wrapper class, 포장 클래스)라 합니다. 래퍼(포장) 클래스의 생성자는 매개변수로 __문자열__ 이나 각 __자료형__ 의 값들을 인자로 받습니다.   
   
   | 기본 타입 |래퍼 클래스<br>(포장 클래스)|
   |:-------:|:-------:|
   | byte | Byte |
   | char | Character |
   | short | Short |
   | int | Integer |
   | long | Long |
   | float | Float |
   | double | Double |
   | boolean | Boolean|

1. # 박싱과 언박싱
   기본형 타입의 값을 포장 객체로 만드는 과정을 박싱이라 하고, 반대로 포장 객체에서 기본 타입의 값을 구하는 과정을 언박싱이라고 합니다.   
   ```java
      Byte b1 = new Byte(10);
      Byte b2 = new Byte("10");

      Short s1 = new Short(10);
      Short s2 = new Short("10");

      Integer i11 = new Integer(100);
      Integer i21= new Integer("100");

      Long l11 = new Long(100);
      Long l21 = new Long("100");

      Float f1 = new Float(10.0);
      Float f2 = new Float(10.0f);
      Float f3 = new Float("10.0");

      Double d1 = new Double(1.0);
      Double d2 = new Double("1.0");

      Character c = new Character('a');
   ```   
   하지만 위에 방법을 권장하지는 않습니다.   
   Integer(int)' is deprecated since version 9 and marked for remova.      
   It is rarely appropriate to use this constructor. The static factory valueOf(int) is generally a better choice, as it is likely to yield significantly better space and time performance.   

   new 생성자를 이용해 래퍼 클래스를 생성하기 보단 valueOf 메서드를 사용할 것을 권장하고 있습니다.

   ```java
   
   
   ```

1. # 