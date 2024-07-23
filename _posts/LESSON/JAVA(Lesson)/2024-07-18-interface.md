---
layout: single
title: 07_18.인터페이스
categories: JAVA(Lesson)
tag: []
author_profile: false
---

1. # 작성법
   모든 멤버변수는 public static final 이어야 하며, 이를 생략할 수 있습니다.   
   모든 메소드는 public abstract 이어야 하며, 이를 생략할 수 있습니다.   
   
   ```java
      interface interfaceEx{
         public static final int a =14;
         public int e = 33;	//public static final int e = 33;
         static int c = 54;	//public static final int c = 54;
         final int d = 1;	   //public static final int d = 1;
         int b = 12;			   //public static final int b = 12;
         
         public abstract void method();   
         public void method2();           //public abstract void method2();
         abstract void method3();         //public abstract void method3();
         void method4();                  //public abstract void method4();
      }
   ```   

1. # 인터페이스
   1.인터페이스는 상수와 추상 메소드로 구성되어 있다. 자바 8부터 디폴트 메소드, 정적 메소드도 사용 가능   
   ```java
      public interface Inter01{
         int a = 10;    //상수(public static final 생략 가능)
         void check();  //추상메소드(public abstract 생략 가능)
      }
   ```   

   2.인터페이스를 상속 받을 때는 implements로 상속을 받는다.   

   3.인터페이스를 상속 받은 일반 클래스는 인터페이스 안에 들어있는 추상 메소드를 반드시 Method Overriding 해야 한다
   ```java
      interface A{
         public abstract void check();
      }

      class S implements A{
         public void check(){}      //public을 생략할 수 없다.
      }
   ```

   4.인터페이스는 다중 상속을 허용한다.   
   ```java
      interface A{}
      interface B{}
      class S implements A,B{}
   ```

   5.추상 클래스와 인터페이스를 모두 상속을 받는 경우에는 추상 클래스를 먼저 상속을 받고, 인터페이스는 그 다음으로 상속 받아야 한다(상속 받는 순서가 바뀌면 안됨)
   ```java
      interface A{}
      abstract class B{}
      class S extends B implements A{}
   ```  
   클래스(추상 클래스 포함) 먼저 상속받고 이후에 인터페이스를 상속   

   6.인터페이스끼리 상속을 받을 때는 extends로 상속 받는다.   
   ```java
      interface A{}
      interface B{}
      interface C extends A,B {}
   ```  
   상속 받은 인터페이스에선 메소드 오버라이딩을 할 수 없다. 인터페이스는 일반 메소드를 가질 수 없다. 

   인터페이스도 클래스처럼 1개당 바이트코드가 만들어진다.


