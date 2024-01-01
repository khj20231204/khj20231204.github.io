---
layout: single
title: 중첩 클래스
categories: JAVA
tag: []
---

1. # 중첩 클래스
   클래스와 밀접한 관계가 있는 클래스를 클래스 내부에 선언하는 것을 말하며, 이들 클래스와 관계없는 외부에서 불필요한 클래스의 접근을 제한하며 코드의 복잡성을 줄일 수 있습니다.   
   
   ```java
      public class A { //A클래스 선언
    
         public A(){ ... }  //A클래스 생성자
         
         class B{ ... }  //A클래스와 밀접한 관계가 있는 인스턴스 멤버 클래스 B
         
         static class C{ ... }  //A클래스와 밀접한 관계가 있는 정정 멤버 클래스 C
         
         void method(){
            class D{ ... }  //A클래스의 메소드 안에 선언된 로컬 클래스 D
         }
      }
   ```   
   멤버 클래스 : class B, static class C   
      class B - 인스턴스 멤버 클래스, static class C - 정적 멤버 클래스   
   로컬 클래스(메소드 내부에서 선언) : class D   

   A클래스 안에 모든 중첩 클래스들은 A클래스가 존재해야 사용가능.   

1. # 멤버 클래스
   ```java   
      public class A {

         class B{  //인스턴스 멤버 클래스 
            B(){
                  System.out.println("B constructor");
            }

            int i;  //필드
            static int j;  //정적 필드
            void method(){  //메소드
                  System.out.println("B class's method");
            }
            static void method2(){  //정적 메소드
                  System.out.println("B class static method2");
            }
         }

         static class C{  //정적 멤버 클래스
            C(){
                  System.out.println("static C constructor");
            }

            int i;  //필드
            static int j;  //정적 필드
            void method(){  //메소드
                  System.out.println("C class's method");
            }
            static void method2(){  //정적 메소드
                  System.out.println("C class static method2");
            }
         }
      }
   ```   
   클래스 내부에 바로 선언되는 클래스로   
   static이 붙지 않은 인스턴스 멤버 클래스, static이 붙은 정적 멤버 클래스로 구분 됩니다.   

   인스턴스 객체에서 필드, 정적 필드, 메소드, 정적 메소드 모두 접근 가능합니다.   
   정적 객체에서도 필드, 정적 필드, 메소드, 정적 메소드 모두 접근 가능합니다.   

   A 클래스 외부에서 호출   
   ```java
      //A class
      A a = new A();  //A constructor

      //instance B class
      A.B b = a.new B();  //B constructor
      b.i = 11;
      A.B.j = 22;
      b.method();  //B class's method
      A.B.method2();  //B class static method2

      //static C class
      A.C c = new A.C();  //static C constructor
      c.i = 33;
      A.C.j = 44;
      c.method();  //C class's method
      A.C.method2(); //C class static method2
   ```   
   필드와 메소드는 객체를 만들어서 접근하고, 정적 필드와 메소드는 클래스에서 바로 접근합니다.   

   컴파일 시 $만 붙어서 표시되는 바이트 코드 파일(.class)이 별도로 생성됩니다.   
   예)A $ B .class  //A 바깥 클래스 , B 내부 클래스   

1. # 로컬 클래스
   ```java
      //A 클래스
      public class A {  //A constructor

         //**로컬 클래스는 접근 제한자와 static을 붙일 수 없음

         void methodA(){  // ---------------------- 메소드
            class D{  //인스턴스 로컬 클래스
                  D(){
                     System.out.println("D constructor");
                  }
                  int i;  //필드
                  static int j;  //정적 필드
                  void method(){  //메소드
                     System.out.println("D class's method");
                  }
                  static void method2(){  //정적 메소드
                     System.out.println("D class static method2");
                  }
            }

            D d = new D();  //D constructor
            d.i = 55;
            D.j = 66;
            d.method();  //D class's method
            D.method2();  //D class static method2
         }

         static void staticMethodA(){  // ---------------------- 정적 메소드
            class E{  //인스턴스 로컬 클래스 
                  E(){
                     System.out.println("E constructor");
                  }
                  int i;  //필드
                  static int j;  //정적 필드
                  void method(){  //메소드
                     System.out.println("E class's method");
                  }
                  static void method2(){  //메소드
                     System.out.println("E class static method2");
                  }
            }

            E e = new E();  //E constructor
            e.i = 77;
            E.j = 88;
            e.method();  //E class's method
            E.method2();  //E class static method2
         }
      }
   ```
   클래스의 생성자나 메소드 내부에 선언된 클래스로 생성자나 메소드가 실행될 때만 사용   
   
   컴파일 시 $1이 표시되는 바이트 코드 파일(.class)이 별도로 생성됩니다.   
   예)A $1 B .class  //A 바깥 클래스, B 내부 클래스    

   호출 시   
   ```java

   ```
