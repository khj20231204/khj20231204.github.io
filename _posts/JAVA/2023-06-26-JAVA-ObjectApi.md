---
layout: single
title: Object클래스
categories: JAVA
tag: [object,equals,문자열 리터럴,toString]
---

1. ## Object클래스
   Object클래스는 모든 클래스의 최상위 클래스입니다. 아무것도 상속 받지 않으면 자동으로 Object를 상속받기 때문에, Object가 가지고 있는 메소드는 모든 클래스에서 사용할 수 있습니다.
1. ## equals(Object obj)
   1. 
   - equals는 객체를 비교하는 메서드입니다.
   - 비교연산자인 ==과 동일한 결과를 리턴합니다.
   - 객체의 참조변수를 받아서 주소값을 비교합니다.
   ```java
   char[] c1 = {'a','b','c'};
   char[] c2 = {'a','b','c'};
   System.out.println(c1.equals(c2)); //false
   System.out.println(c1 == c2); //false
   ```
   데이터 값은 'a','b','c'로 동일하지만 c1과 c2의 주소값이 다르기 때문에 false를 리턴합니다.
   ```java
      public class ObjectApi {
         class A {
         }

         class B extends A {
         }

         public void objectFunc() {
            A a = new A();
            B b = new B();
            System.out.println(b.equals(a)); //false
            A c = b;
            System.out.println(b.equals(c)); //true
         }
      }    
   ```
   클래스B는 클래스A를 상속받았지만 생성된 주소값이 a와 b가 서로 다르기 때문에 false를 리턴합니다.
   변수 c는 선언은 클래스A로 선언했지만, 대입된 객체의 주소값이 b이기 때문에 true를 리턴합니다.
   1. 예외 String클래스의 equals()메서드
   - String클래스가 Object의 equals()메서드를 재정의 했기 때문에 번지 비교가 아닌 문자열 비교를 합니다
   ```java
      String str_1 = new String("abc");
      String str_2= new String("abc");
      System.out.println(str_1.equals(str_2)); //true
      System.out.println(str_1 == str_2); //false
   ```
   str_1과 str_2의 문자열값이 "abc"로 같기 때문에 equals메서드는 true를 리턴합니다. 하지만 연산자 "=="는 재정의(override) 하지 않았기 때문에 주소값을 비교하고 false를 리턴합니다.
   1. 문자열 리터럴 " "
   + 자바에서 문자 리터럴(데이터)은 클래스 파일 안에 리터럴 목록이 따로 존재합니다. 이 목록이 클래스 로더에 의해 메모리에 올라갈 때 JVM에 의해 Runtim Data Area(JVM 메모리영역)내부의 메소드 영역인 constant pool에 저장이 됩니다. 
   + constant pool에는 "abc"란 문자열이 하나가 있고 이 주소값이 "abc"를 저장하는 모든 객체변수에 저장이 됩니다.
   ```java
      String str1 = "abc";
      String str2 = "abc";
      System.out.println(str1.equals(str2)); //true
      System.out.println(str1 == str2); //true
   ```
   str1과 str2이는 constant pool에 있는 1개의 "abc" 같은 주소값을 할당 받습니다.
   1. 보통 equqls()메서드는 바로 사용하지 않고 <span style="color:red"> __override__ 를 해서 사용합니다.</span>
1. ## toString
   1. 객체에 대한 정보를 클래스 이름과 해시코드로 나타냅니다.
   ```java
      ObjectApi oa = new ObjectApi();
      oa.objectFunc();
      System.out.println(oa.toString()); //api_class.ObjectApi@2f4d3709 패키지.클래스이름@해시코드
   ```
   1. String클래스는 String인스턴스가 갖고 있는 문자열을 반환하도록 오버라이딩되었습니다.
   ```java
      String str = new String("abcd");
      System.out.println(str.toString()); //abcd
   ```
   1. Date클래스는 날짜와 시간을 반환하도록 오버라이딩되었습니다.
   ```java
      Date date = new Date();
      System.out.println(date.toString()); //Mon Jun 26 23:15:06 KST 2023
   ```
   1. 보통 toString()메서드는 바로 사용하지 않고 <span style="color:red"> __override__ 를 해서 사용한다.</span>
