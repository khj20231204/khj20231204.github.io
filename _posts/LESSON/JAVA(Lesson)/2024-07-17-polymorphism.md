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


1. # ProductEx 예제

   Product computer = new Computer();   
   <span style="color:red">타입 참조변수 = new연산자 인스턴스</span>   
   Product는 참조변수의 타입   

   Computer가 Product를 상속 받았을 때   
   ```
      Product computer = new Computer();   ---①
      Computer computer2 = new Computer(); ---②
   ```   
   의 차이점   
   멤버변수가 조상 클래스와 자손 클래스에 중복으로 정의된 경우,   
   ① : Product의 멤버변수를 사용, 메소드는 자손 Computer의 메소드 사용   
   ② : Computer의 멤버변수를 사용, 메소드는 Computer의 메소드 사용   

   ```java   
      class Product{
         String name = "product";
         int price = 1111;
         
         void printPrice() {
            System.out.println("name:"+ name+ ", price:"+price);
         }
      }

      class Computer extends Product{
         String name = "Computer";
         int price = 300;
         
         @Override
         void printPrice() {
            System.out.println("Computer에서 name:"+ name+ ", price:"+price);
         }
         
         void ComputerMethod() {
            System.out.println("Computer의 Method");
         }
      }

      class LastComputer extends Computer{
         String name = "LastComputer";
         int price = 100000;
         
         @Override
         void printPrice() {
            System.out.println("LastComputer에서 name:"+ name+ ", price:"+price);
         }
         
         void lastComputerMethod() {
            System.out.println("LastComputer의 Method");
         }
      }

      class Buyer{
         
         void buyerPrice(Product p) {
            //필드는 타입의 필드값을 가져온다
            System.out.println("Product변수:" + p.name + " ,"+ p.price);
            //메소드는 인스턴스에서 오버로딩된 메소드를 가져온다
            p.printPrice();  
         }
      }

      public class PrductEx {

         public static void main(String[] args) {
            //타입 참조변수 = new연산자 인스턴스
            Product computer = new Computer();
            Computer computer2 = new Computer();
            
            Buyer buyer = new Buyer();
            buyer.buyerPrice(computer);   //computer는 Product로 업캐스팅
            buyer.buyerPrice(computer2);  //computer2는 Product로 업캐스팅
            
            System.out.println();
            
            Product lastComputer = new LastComputer();
            LastComputer lastComputer2 = new LastComputer();
            
            buyer.buyerPrice(lastComputer);  //lastComputer는 Product로 업캐스팅
            buyer.buyerPrice(lastComputer2); //lastComputer2는 Product로 업캐스팅
         }
      }

      결과값
      Product변수:product ,1111
      Computer에서 name:Computer, price:300
      Product변수:product ,1111
      Computer에서 name:Computer, price:300

      Product변수:product ,1111
      LastComputer에서 name:LastComputer, price:100000
      Product변수:product ,1111
      LastComputer에서 name:LastComputer, price:100000
   ```   
   buyer.buyerPrice(computer);   
   buyer.buyerPrice(computer2);   
   buyerPrice의 매개변수 Product의해 computer와 computer2는 Product로 업캐스팅된 상태에서 전달됩니다.   
   
   System.out.println("Product변수:" + p.name + " ,"+ p.price);   
   멤버변수 name, price는 Product의 name과 price   
   p.printPrice();   
   printPrice는 상속받은 자식의 메소드 호출   

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