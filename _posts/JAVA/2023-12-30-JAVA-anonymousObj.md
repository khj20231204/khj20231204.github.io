---
layout: single
title: 익명 객체 / 익명 구현 객체
categories: JAVA
tag: []
---

1. # 익명 객체
   클래스나 인터페이스를 상속받는 자식 클래스나 구현 클래스를 만들지 않고 부모 클래스나 인터페이스를 가져와서 바로 자식 객체나 구현 개체를 생성할 수 있습니다. 선언과 객체의 생성을 동시에 하기 때문에 한번만 사용될 수 있고, 오직 하나의 객체만 생성할 수 있습니다.   
   오버라이딩과 기타 사용 방법은 동일하며 부모 클래스와 인터페이스 이후에 바로 객체를 생성하는 방법입니다.   

   일반적으로
   ```java

      class A{
         ...
      }

      class B extends A{
         ...
      }
   ```   
   A를 상속받는 B클래스를 만들게 됩니다. 하지만   
   ```java
      class A{
         ...
      }

      class B{
         A a = new A(){  //익명 객체 생성
            ...
            //여기에 상속받은 A기능을 구현
            void func(){

            }
            ...
         }
      }
   ```   
   A a = new A(){...} 란
   A a = new A()는 "new연산자를 이용해서 A클래스로 a객체를 생성하라"란 명령어입니다.   
   하지만 뒤에 { }로 해당 내용을 구현할 수 있는 중괄호가 놓이게 되면   
   "A클래스를 __상속__ 받아 new연산자로 { } 안에 내용으로 a란 객체를 __A클래스 타입으로 생성__ 하라"란 명령어가 됩니다.   
   위의 예에서 a객체는 필드 변수가 됩니다.   

   main에서 호출을 할 땐
   ```java
      B b = new B();
      b.a.func();
   ```   
   이런 식으로 호출을 할 수 있습니다.

1. # 익명 객체 사용
   익명 객체는 필드, 메소드 안에서 변수, 메소드의 매개변수로 이용될 수 있습니다.
   ```java
      public class Person {
         void wake(){
            System.out.println("Wake Up at Six");
         }
      }
   ```   
   3가지의 경우 오버라이딩을 위해 사용될 Person클래스 입니다. 익명 객체도 상속받는 것과 같이 메소드를 오버라딩이해서 사용하게 됩니다.   

1. # 필드에서 익명 객체 사용 예
   ```java
      public class AnonymousObj {
      //필드에서 익명 객체 사용 예
      Person person = new Person(){  //Person을 선언 후 바로 { }로 정의

         void fieldAnonymousObj(){
            System.out.println("필드에서 익명 객체 사용");
         }

         @Override
         void wake() {  //Person클래스의 wake 오버라이딩
            System.out.println("Wake Up at Seven");
            fieldAnonymousObj();
         }
      };
   ```   
   main에서 호출 방법
   ```java
      public static void main(String[] args){
         AnonymousObj ao = new AnonymousObj();
         ao.person.wake(); //ao객체 안에 person필드에서 정의된 wake메소드
      }
   ```   
   ao객체의 person필드에서 재정의된 wake메소드를 호출합니다. 현재 ao객체는 Person클래스 타입이기 때문에 익명 객체 안에서 정의된 __fieldAnonymousObj메소드__ 에 __직접적으로 접근을 할 수 없습니다__.
   그렇기 때문에 오버라이딩된 wake메소드 안에서 fieldAnonymousObj()를 호출하게 됩니다.   

1. # 메소드 내부에서 변수로 익명 객체 사용 예
   메소드 내부에서 지역 변수로 익명 객체가 사용됩니다.   

   ```java
      public class AnonymousObj {
      //메소드 내부에서 변수로 익명 객체 사용 예
      void methodObj(){
         //익명 객체로 변수 선언
         Person localVar = new Person(){
            void methodAnonymousObj(){
                  System.out.println("메소드 내부 변수로 익명 객체 사용");
            }

            @Override
            void wake() {
                  System.out.println("Wake Up ad eight");
                  methodAnonymousObj();
            }
         };
         localVar.wake();
      }
   ```   
   Person localVar = new Person(){ ... } localVar이란 변수를 선언 후 { }로 익명 객체를 선언합니다.   
   localVar.wake() 마지막에 localVar로 wake메소드를 호출 합니다.   

    main에서 호출 방법   
    ```java
      public static void main(String[] args){
         AnonymousObj ao = new AnonymousObj();
         ao.methodObj();
      }
    ```

1. #  매개변수로 익명 객체 사용 예
   ```java
      public class AnonymousObj {
            void methodParamObj(Person p){
            p.wake();
         }
      }
   ```   
   methodParamObj메소드의 매개변수 값으로 Person클래스를 받는데 main에서 전달할 때 익명 객체를 선언하게 됩니다.   

   main에서 호출 방법
   ```java
      public static void main(String[] args){

        AnonymousObj ao = new AnonymousObj();
      
        //매개변수로 전달할 익명 객체
        ao.methodParamObj(new Person(){  //Person클래스를 상속받아 구현
                void paramAnonymousObj(){
                    System.out.println("매개변수로 전달되는 익명 객체");
                }
                @Override
                void wake() {
                    System.out.println("Wake Up at nine");
                    paramAnonymousObj();
                }
            }
        );
   ```   
   ao.methodParamObj(new Person(){ ... }); person클래스를 상속받아 새로운 메소드를 만들 수도 있고, 기존 메소드를 재정의 할 수도 있습니다. 익명 객체를 바로 정의하면서 methodParamObj메소드의 매개값으로 넘겨주게 됩니다.   
   methodParamObj메소드가 정의된 AnonymousObj클래스에선 Person클래스 타입으로 값을 받기 때문에 익명 객체에서 정의된 paramAnonymousObj메소드에 바로 접근을 할 수 없습니다.   
   그렇기 때문에 
   ```java
      void methodParamObj(Person p){
            p.wake();
      }
   ```   
   p.wake()로 전달받은 매개변수 값인 Person클래스에 있는 wake메소드를 호출하게 됩니다.   
   

1. # 구현 객체
   인터페이스를 선언 후 클래스에서 상속받아 해당 클래스로 구현 객체를 생성해서 사용하는 것이 일반적인 방식이지만 일회성으로 바로 인터페이스를 사용할 수도 있습니다. 익명 객체에서 사용했던과 같은 방식으로 필드에서 정의, 메소드 안에서 변수로 정의, 메소드의 매개변수로 정의. 이렇게 3가지로 인터페이스의 구현 객체를 바로 정의해서 사용할 수 있습니다.   

   RemoteControl이란 인터페이스를 선언합니다.   
   ```java
      public interface RemoteControl {
         public void turnOn();
         public void turnOff();
      }
   ```   

   Anonymous에서 인터페이스를 implement하지 않고 바로 구현 객체를 생성합니다.   
   ```java
      public class Anonymous {
         //필드에서 정의
         RemoteControl rcField = new RemoteControl() {  
            @Override
            public void turnOn() {
                  System.out.println("TV On");
            }

            @Override
            public void turnOff() {
                  System.out.println("TV Off");
            }
         };

         //메소드 내에서 변수로 정의
         void method(){
            RemoteControl rcLocalVar = new RemoteControl() {
                  @Override
                  public void turnOn() {
                     System.out.println("Audio On");
                  }

                  @Override
                  public void turnOff() {
                     System.out.println("Audio Off");
                  }
            };

            rc  
         }

         //메소드의 매개변수로 정의
         void method2(RemoteControl rcParam){
            rcParam.turnOn();
         }
      }
   ```

   main에서 호출 시
   ```java
      public static void main(String[] str){

        Anonymous anony = new Anonymous();  //anony란 객체를 생성
        anony.rcField.turnOn();  //필드로 인터페이스의 구현 객체 호출
        anony.rcField.turnOff();  //필드로 인터페이스의 구현 객체 호출

        anony.method();  //메소드로 method메소드 안에 구현된 객체 호출

        RemoteControl rc = new RemoteControl() {  //main에서 바로 구현객체 생성
            @Override
            public void turnOn() {
                  ...
            }

            @Override
            public void turnOff() {
                  ...
            }
        };

        anony.method2(rc);  //anony객체 메소드의 매개변수로 전달
        rc.turnOff();  //바로 오버라이딩된 메소드 호출
    }
   ```