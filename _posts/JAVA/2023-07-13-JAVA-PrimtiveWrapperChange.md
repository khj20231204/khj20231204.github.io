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

   new연산자를 사용해 객체생성을 할 수 있습니다. 다음은 박싱예제 입니다.
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

   new 생성자를 이용해 래퍼 클래스를 생성하기 보단 valueOf 메소드를 사용할 것을 권장하고 있습니다.  
   ```java
      
      //박싱 예제

      Byte b1_fix = 10;  //값을 입력 받아 박싱 - 자동 박싱(오토 박싱)
      Byte b2_fix = Byte.valueOf("10");  //valueOf로 박싱

      Short s1_fix = 10;
      Short s2_fix = Short.valueOf("10");

      Integer i1_fix = 100;
      Integer i2_fix = Integer.valueOf("100");

      Long l1_fix = 100l;
      Long l2_fix = Long.valueOf("100l");

      Float f1_fix = 10.0f;
      Float f2_fix = Float.valueOf("10.0f");

      Double d1_fix = 1000d;
      Double d2_fix = Double.valueOf("1000d");

      Character c_fix = 'c';
      Character c2_fix = Character.valueOf('c');
   ```   
   vlueOf메소드는 인자로 문자열을 받습니다.   
   
   vlueOf메소드는 10진수 뿐만 아니라 다른 진법의 숫자일 때도 변환이 가능합니다.   
   ```java
      Integer idx_i4 = Integer.valueOf("100",2); //4
      Integer idx_i5 = Integer.valueOf("100",8); //64
      Integer idx_i6 = Integer.valueOf("100",16); //256
   ```   

   언박싱은 '기본타입+Value()'메소드를 사용하면 됩니다.   
   ```java

      //언박싱 예제

      byte b = b2_fix.byteValue();

      short s = s2_fix.shortValue();

      int i = b2_fix.intValue();

      long l = l2_fix.longValue();

      float f = f2_fix.floatValue();

      double d = d2_fix.doubleValue();

      char c = c2_fix.charValue();
   ```   

   문자열을 기본형으로 변경할 땐 parse+기본타입을 사용합니다.   
   ```java
      byte bp = Byte.parseByte("100");

      Short sp = Short.parseShort("100");

      int ip = Integer.parseInt("100");

      long lp = Long.parseLong("100");

      float fp = Float.parseFloat("100");

      double dp = Double.parseDouble("100");
    ```
    
    pasrse역시 다른 진법의 숫자로 표현할 수 있습니다.
    ```java    
      int idx_i1 = Integer.parseInt("100",2); //4, 2진수로 표현
      int idx_i2 = Integer.parseInt("100",8); //64, 8진수로 표현
      int idx_i3 = Integer.parseInt("100",16); //256, 16진수로 표현
   ```
1. # 자동 박싱
   valueOf나 intValue를 사용하지 않고 자동으로 박싱과 언박싱이 일어나기도 합니다. 자동 박싱은 포장 클래스 타입에 기본값이 대입된 경우 일어나고, 자동 언박싱은 기본 타입에 포장 클래스 타입이 대입된 경우 일어납니다.   
   예를 들어 int 타입의 값을 Integer클래스 변수에 대입하면 자동 박싱이 일어나고, Integer객체를 int타입 변수에 대입하거나, Integer 객체와 int 값을 연산하면 자동 언박싱이 일어납니다.   
   ```java
      Integer obj = 4;  //자동 박싱

      int val = obj;  //자동 언박싱
      int val2 = obj + 10;  //자동 언박싱
   ```

1. # == 와 equal
   "==" 연산자는 비교 값들의 주소 값을 비교하고, 래퍼 클래스에서 사용하는 equal는 값 자체를 비교하도록 오버라이딩 되어있습니다. 일반적으로 주소 값을 비교하는 일은 드물고 값을 비교하기 때문에 == 보단 equal을 사용해야합니다.   
   ```java
      Integer val1 = 300;
      Integer val2 = 300;

      System.out.println(val1 == val2);  //false
      System.out.println(val1.equals(val2));  //true
   ```