---
layout: single
title: 07_17.추상 클래스
categories: JAVA(Lesson)
tag: []
author_profile: false
---

1. # 추상 클래스(공통 코드)
   공통 코드 - 필드, 메소드   
   추상 클래스는 추상 메소드를 가지고 있으며, 상속 받은 클래스들은 추상 메소드를 필수 오버라이딩 해야 합니다.   

   1)추상 클래스는 자체적으로 객체를 생성할 수 없다.   
   ```java
      public abstract class AbsClass{

      }
   ```   

   2)추상 클래스를 구성하는 요소는 필드, 생성자, 메소드, __추상 메소드__   
   *추상 메소드 : 이름만 있고 내용이 없다   
   ```java
      public abstract class AbsClass{
         int a = 10;             //필드
         abstract void Method(); //추상 메소드
         void Method2(){         //일반 메소드

         }
      }
   ```   

   3)추상 클래스를 상속 받을 때는 extends를 이용해서 상속을 받는다.   

   4)추상 클래스를 상속받은 일반 클래스는 추상클래스 안에 들어있는 추상 메소드를 반드시 Method Overriding 해야 한다.   

   5)추상 클래스를 상속받은 일반 클래스는 추상 클래스 안에 들어있는 추상 메소드를 반드시 Method Overriding 해야 한다.   

   6)추상 클래스도 단일 상속만 가능하다(클래스의 다중 상속을 허용하지 않는다)   

1. # 추상 클래스가 추상 클래스를 상속
   미들 클래스에서 오버라이딩하든 마지막 클래스에서 오버라이딩하든 최소 한군데에선 오버라이딩을 해야한다   

   미들 클래스에서 오버라이딩을 하는 경우   
   ```JAVA
      abstract class AbstractClass{				//추상 클래스
         abstract void Method01();				//추상 메소드
               void Method02() {						//일반 메소드
                  System.out.println("Method02 : 추상 클래스에서 구현"); 
               }
            }

      abstract class MiddleClass extends AbstractClass{	//추상 클래스가 추상 클래스를 상속받을 때도 extends
         public void Method03() {
            System.out.println("Method03 : 추상 클래스에서 구현");
         }
         @Override
         void Method01() {    //<---------------------------------미들 클래스에서 오버라이딩
            System.out.println("Method01 : 자식 클래스에서 메소드 오버라이딩한 메소드");
         }
      }

      class SubClass extends MiddleClass{

      }

   ```

   최종 클래스에서 오버라이딩을 하는 경우   
   ```java
      abstract class AbstractClass{				//추상 클래스
      abstract void Method01();				   //추상 메소드
            void Method02() {						//일반 메소드
               System.out.println("Method02 : 추상 클래스에서 구현"); 
            }
         }

      abstract class MiddleClass extends AbstractClass{	//추상 클래스가 추상 클래스를 상속받을 때도 extends
         public void Method03() {
            System.out.println("Method03 : 추상 클래스에서 구현");
         }
      }

      class SubClass extends MiddleClass{
         @Override
         void Method01() {  //<----------------------------------------최종 클래스 오버라이딩
            System.out.println("Method01 : 자식 클래스에서 메소드 오버라이딩한 메소드");
         }
      }
   ```

1. # 메소드 오버라이딩(형상화)
   ```java
      abstract class ShapeClass{			//부모 클래스
         abstract void draw();			//추상 메소드
      }

      class Circ extends ShapeClass{		//자식 클래스

         @Override
         public void draw() {			//메소드 오버라이딩
            System.out.println("원을 그린다.");
         }
      }

      class Tria extends ShapeClass{		//자식 클래스	

         @Override
         public void draw() {
            System.out.println("삼각형을 그린다.");
         }
      }

      class React extends ShapeClass{		//자식 클래스

         @Override
         public void draw() {			//메소드 오버라이딩
            System.out.println("사각형을 그린다");
         }
      }

      public class AbstractTest04 {

         public static void main(String[] args) {
            ShapeClass c = new Circ();		//업캐스팅 - 자동형변환
            ShapeClass t = new Tria();		//업캐스팅 - 자동형변환
            ShapeClass r = new React();		//업캐스팅 - 자동형변환
            
            c.draw();
            t.draw();
            r.draw();
            }
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
