---
layout: single
title: SPRING_BEGINNER
categories: SPRING_MASTER
tag: []
author_profile: false
---
 
1. # redirect  

1. # IOC와 DI
   IOC : 설계 원칙 > DI : 디자인 패턴   
   
   김치 볶음밥 맛있게 만드는 방법(설계 원칙 - IOC)   
   1.신선한 재료를 사용한다.   
   2.신 김치를 사용한다.   
   3.밥과 김치의 비율을 잘 맞춘다.   
   => 원칙으로 원론적인 부분   

   김치 볶음밥 레시피(디자인 패턴 - DI)   
   1.오일을 두른 팬에 파를 볶아 파기름을 만든다.   
   2.준비한 햄을 넣고 볶다가, 간장을 때리 붓는다.   
   3.미리 식혀 둔 밥을 넣고 함께 볶는다.   
   => 실제 구현된 방법( ≒ 패턴)   

1. # 의존성
   의존성 - 강한 결합과 약한 결합 => 다형성   

   __1.강한 결합__   
   ```java
      public class Consumer {

         void eat() {
            Chicken chicken = new Chicken();  // 여기 부분
            chicken.eat();  // 여기 부분
         }

         public static void main(String[] args) {
            Consumer consumer = new Consumer();
            consumer.eat();
         }
      }

      class Chicken {
         public void eat() {
            System.out.println("치킨을 먹는다.");
         }
      }
   ```   
   현재 eat에 Chicken이 있는데 Chicken대신 카레, 짬뽕, 피자,.. 등으로 메뉴가 바뀌면 eat메소드 내부 코드를 다 바꿔야 한다.   

   __2.약한 결합__   
   ```java   
      public class Consumer {

         void eat(Food food) { // 여기 이 부분
            food.eat();
         }

         public static void main(String[] args) {
            Consumer consumer = new Consumer();
            consumer.eat(new Chicken());
            consumer.eat(new Pizza());
         }
      }

      interface Food { // 여기 이 부분
         void eat();
      }

      class Chicken implements Food{
         @Override
         public void eat() {
            System.out.println("치킨을 먹는다.");
         }
      }

      class Pizza implements Food{
         @Override
         public void eat() {
            System.out.println("피자를 먹는다.");
         }
      }
   ```   
   인터페이스를 매개변수로 할당해 다형성을 이용   

1. # 주입   
   객체를 객체에 할당하는 것   
   필드, 메소드, 생성자를 통한 주입 => 인터페이스, 오버로딩 사용   

   __1.필드에 직접 주입__   
   ```java
      public class Consumer {

         Food food; // 인터페이스 Food를 필드로 선언

         void eat() {
            this.food.eat();
         }

         public static void main(String[] args) {
            Consumer consumer = new Consumer();
            consumer.food = new Chicken(); //필드로 선언된 food객체에 직접 치킨 객체 주입
            consumer.eat();

            consumer.food = new Pizza(); //필드로 선언된 food객체에 직접 피자 객체 주입
            consumer.eat();
         }
      }

      interface Food {
         void eat();
      }

      class Chicken implements Food{
         @Override
         public void eat() {
            System.out.println("치킨을 먹는다.");
         }
      }

      class Pizza implements Food{
         @Override
         public void eat() {
            System.out.println("피자를 먹는다.");
         }
      }
   ```   

   __2.메서드를 통한 주입__   
   ```java
      public class Consumer {

         Food food;

         void eat() {
            this.food.eat();
         }

         public void setFood(Food food) { //set메서드의 매개변수로 Food 선언
            this.food = food;
         }

         public static void main(String[] args) {
            Consumer consumer = new Consumer();
            consumer.setFood(new Chicken()); //set메서드를 이용하여 치킨 객체 주입
            consumer.eat();

            consumer.setFood(new Pizza()); //set메서드를 이용하여 피자 객체 주입
            consumer.eat();
         }
      }

      interface Food {
         void eat();
      }

      class Chicken implements Food{
         @Override
         public void eat() {
            System.out.println("치킨을 먹는다.");
         }
      }

      class Pizza implements Food{
         @Override
         public void eat() {
            System.out.println("피자를 먹는다.");
         }
      }
   ```   

   __3.생성자를 통한 주입__   
   ```java
      public class Consumer {

         Food food;

         public Consumer(Food food) { //Consumer 생성자의 매개변수로 Food 선언
            this.food = food;
         }

         void eat() {
            this.food.eat();
         }

         public static void main(String[] args) {
            Consumer consumer = new Consumer(new Chicken()); // 생성자에 치킨 객체 주입
            consumer.eat();

            consumer = new Consumer(new Pizza()); // 생성자에 피자 객체 주입
            consumer.eat();
         }
      }

      interface Food {
         void eat();
      }

      class Chicken implements Food{
         @Override
         public void eat() {
            System.out.println("치킨을 먹는다.");
         }
      }

      class Pizza implements Food{
         @Override
         public void eat() {
            System.out.println("피자를 먹는다.");
         }
      }
   ```


   



   



