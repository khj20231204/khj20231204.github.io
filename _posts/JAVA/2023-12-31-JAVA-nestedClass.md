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
   메소드 안에서 정의되는 로컬 클래스는 접근 제한자(public, private)과 static을 붙일 수 없습니다. 로컬 클래스는 메소드 내부에서만 사용되기 때문에 외부의 접근을 제한할 필요가 없습니다.  
   필드, 메소드, 정적 필드, 정적 메소드에 모두 접근이 가능합니다.   

   A 클래스 외부에서 호출   
   ```java
      A a = new A();
      //D class
      a.methodA();

      //E class
      A.staticMethodA();
   ```   
   외부에서 로컬 클래스를 바로 접근할 수 없습니다. 로컬 클래스는 메소드 내부 안에서만 사용할 수 있습니다. 따라서 외부에서는 메소드만 호출 하고 
   ```java
      void methodA(){ 
            class D{  
                ...
            }

            D d = new D();  //D constructor
            d.i = 55;
            D.j = 66;
            d.method();  //D class's method
            D.method2();  //D class static method2
         }

         static void staticMethodA(){  
            class E{ 
                  ...
            }

            E e = new E();  //E constructor
            e.i = 77;
            E.j = 88;
            e.method();  //E class's method
            E.method2();  //E class static method2
         }
      }
   ```
   메소드 안에서 객체를 생성 후 필드나 메소드에 접근하게 됩니다.   

   컴파일 시 $1이 표시되는 바이트 코드 파일(.class)이 별도로 생성됩니다.   
   예)A $1 B .class  //A 바깥 클래스, B 내부 클래스    

1. # static의 사용 제한
   필드와 정적 필드, 메소드와 정적 메소드, 클래스와 정적 클래스 서로 간에 데이터를 사용하는데 제한이 따릅니다.   
   필드나 메소드에서 클래스를 사용 시   
   클래스 안에서 필드와 메소드를 사용 시   
   static을 사용하는 할 때 주의 사항이 있습니다.   

1. # 필드나 메소드에서 클래스를 사용 시
   클래스를 선언 후 필드나 메소드에서 선언 한 클래스를 사용할 때 static이 붙은 경우와 붙지 않은 경우 주의 할 점이 있습니다.   

   instance : static 멤버를 사용 가능   
   static : instance 멤버를 사용 못 함   

   인스턴스로 생성할 InstanceClass를 선언, 정적 클래스 MyStaticClass를 선언 후
   각각 필드, 메소드 내부, 정적 메소드 내부 에서 사용될 때 주의 사항이 있습니다.   
   ```java
      public class FieldMethodUseClass {
         //필드나 메소드에서 클래스를 사용시 주의 점
         class InstanceClass{}  //사용될 클래스 선언
         static class MyStaticClass{ }  //사용될 정적 클래스 선언

         //① 필드로 사용
         InstanceClass uc = new InstanceClass();  //필드로 클래스 사용
         MyStaticClass sc = new MyStaticClass();  //필드로 정적 클래스 사용

         //② 메소드 내부
         void instanceMethod(){
            InstanceClass uc = new InstanceClass();  //메소드 내 클래스 사용
            MyStaticClass sc = new MyStaticClass();  //메소드 내 정적 클래스 사용
         }

         //③ 정적 메소드 내부
         static void staticMethod(){
            //InstanceClass uc = new InstanceClass();  error instance멤버 사용 못 함
            MyStaticClass sc = new MyStaticClass();  //정적 메소드 내 정적 클래스 사용
         }
      }
   ```   
   인스턴스에서 정적 멤버를 사용할 수 있기 때문에 필드와 메소드로 선언 시 MyStaticClass 클래스를 사용할 수 있지만 정적 메소드 staticMethod 내부에선 인스턴스 멤버를 사용할 수 없기 때문에 InstanceClass uc = new InstanceClass(); 여기에서 error이 발생합니다.    

1. # 클래스에서 필드나 메소드를 사용
   중첩 클래스 외부에서 선언된 필드나 메소드를 사용시 정적인지 아닌지에 따라 주의할 점이 있습니다. static으로 선언된 멤버는 instance멤버는 static이 선언된 멤버를 instance멤버들을 사용할 수 없습니다.   

   myfield - 필드   
   staticFiled - 정적 필드   
   instanceMethod - 메소드   
   staticMethod - 정적 메소드
   위에 해당 멤버를   
   instanceClass 클래스와 MyStaticClass 정적 클래스에서 각각 사용해 보겠습니다.

   ```java
      public class ClassUseFieldMethod {
         //① 필드  
         int myfield;
         static int staticFiled;

         //② 메소드 
         public void instanceMethod(){}
         public static void staticMethod(){}

         //③ 클래스에서 위에 필드와 메소드를 사용
         class instanceClass{
            void method(){
                  myfield = 10;
                  staticFiled = 11;

                  instanceMethod();
                  staticMethod();
            }
         }
         //④ 정적 클래스에서 위에 필드와 메소드를 사용
         static class MyStaticClass{
            void method(){
                  //myfield = 10;  error static에선 instrann 
                  staticFiled = 11;

                  //instanceMethod();  error
                  staticMethod();
            }
         }
      }
   ```   
   인스턴스 클래스 내부에서 모든 필드와 메소드를 사용할 수 있지만, 정적 클래스 내부에선 정적 멤버만 사용할 수 있습니다. MyStaticClass 클래스에서는 myfield 필드와 instanceMethod 메소드에서 error가 발생했고, 나머지 정적으로 선언된 필드와 메소드는 문제가 없습니다.
