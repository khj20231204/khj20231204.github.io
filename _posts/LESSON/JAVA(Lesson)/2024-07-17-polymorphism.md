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