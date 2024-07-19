---
layout: single
title: 07_17.다형성과 final
categories: JAVA(Lesson)
tag: []
author_profile: false
---

1. # 다형성
   ```java
      class Vehicle{				      //부모 클래스
         String name = "vehicle";
         public void run() {
            System.out.println("차량이 달립니다.");
         }
      }

      class Drive{		
         public void drive(Vehicle vehicle) {	//매개변수의 다형성
            vehicle.run();
            System.out.println(vehicle.name+"가 달린다");
         }
      }

      class Bus extends Vehicle{    //자식 클래스
         public Bus(){
            super.name = "bus";
         }

         @Override
         public void run() {
            System.out.println("버스가 달립니다");
         }
      }

      class Taxi extends Vehicle{	//자식 클래스
         public Taxi(){
            super.name = "taxi";
         }

         @Override
         public void run() {
            System.out.println("택시가 달립니다");
         }
      }

      public class DriveExample {

         public static void main(String[] args) {
            Drive driver = new Drive();
            Bus bus = new Bus();
            Taxi taxi = new Taxi();
            
            //매개변수의 다형성		//업캐스팅(자동 형변환)
            driver.drive(bus);	//Vehicle vehicle = new Bus(); 업캐스팅
            driver.drive(taxi);	//Vehicle vehicle = new taxi(); 업캐스팅
         }
      }
   ```   

1. # Parent p = new Child()
   ```java
      class Parent{
         int a = 10;

         void method() {
            System.out.println("Parent");
         }
      }

      class Child extends Parent{
         int a = 20;
         
         @Override
         void method() {
            System.out.println("Child");
         }

         void method1() {
            System.out.println("Child Method_1");
         }
      }

      public class Polymorphism {

         public static void main(String[] args) {
            Parent p = new Child();
            Child c = new Child();
            
            System.out.println(p.a); 	//10
            p.method();					//child
            //p.method1();				//error
            
            System.out.println(c.a);	//20
            c.method();					//child
            c.method1();				//자식 메소드 호출
         }
      }
   ```   
   Parent p = new Child();   
   __필드__ : 부모P의 필드를 호출   
   __상속 한 메소드__ : 자식 메소드를 호출   
   __자식에게만 있는 메소드__ : 접근 못 함   
   p.method()는 자식에서 오버라이딩한 메소드가 출력되지만, method1()은 자식에게만 있기 때문에 부모에서 접근 불가   

1. # final
   1. final이 멤버변수(필드)에 사용될 경우   
   __상수__ - 값을 수정할 수 없다.   
   ```java
      final int a = 10;
   ```

   2.final이 메소드에 사용될 경우   
   __메소드 오버라이딩__ 을 허용하지 않는다는 의미   
   ```java
      public final void setStr(String s){}
   ```   

   3.final이 클래스에 사용될 경우   
    __상속__ 을 허용하지 않는다는 의미   
   ```java
      final class FinalClass{}
   ```    