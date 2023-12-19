---
layout: single
title: static
categories: JAVA
tag: [static, 정적 멤버]
---

1. # 상속
   기존에 설계되어 있던 클래스에 속성이나 기능 등을 확장하기 위하여 재사용성을 높이고 코드의 중복을 제거하기 위한 방법입니다.    

   기존의 클래스 : __상속하는 클래스__ , 상위 클래스 , 부모 클래스, super class, base class    
   새로운 클래스 : __상속받는 클래스__ , 하위 클래스, 자식 클래스, derived class   

   구현 형태는 다음과 같습니다.   
   ```java
      class Child extends Parent{
         ...
   ```   
   extends 뒤에 오는 클래스는 단 하나의 클래스만 올 수 있습니다.   
   여러개의 클래스가 올 경우 모호성이 발생할 수 있기 때문에 하나의 클래스로 제한을 했습니다. 단 인터페이스는 다중 상속이 가능합니다.   

1. # private인 경우 상속
   Customer클래스에 id를 private두고 VIPCustomer클래스에서 상속 받습니다.
   ```java
      public class Customer {

         private String id;
         public double bonus;
      } 

      public class VIPCustomer extends Customer{

         public VIPCustomer(){
            this.bonus;
            //this.id  ☜ 나타나지 않음
         }
      }
   ```   
   VIPCustomer클래스에서 this 연산자로 접근가능한 변수는 bonus만 허용이 됩니다.
   private 접근 제한자를 사용할 경우 상속받은 클래스에서 접근이 제한됩니다.   
   상속을 하는 경우 접근을 완전 막는 private 대신 외부 클래스에선 접근할 수 없지만, 하위 클래스는 접근 할 수 있는 protected를 사용하면 됩니다.
   부모 크래스와 자식 클래스가 다른 패키지에 존재한다면 default 접근 제한를 갖는 필드와 메소드도 상속 대상에서 제외됩니다.   

1. # 부모 클래스의 생성자 값이 상속받은 자식 클래스에 적용
   ```java

   public class Customer {  //☜ 부모 클래스

      public String grade;

      public Customer(){
         this.grade = "SILVER";
      }
   }

   public class VIPCustomer extends Customer{  //☜ 자식 클래스

      public VIPCustomer(){
         System.out.printf("VIPCustomer의 grade:"+this.grade);
      }
   }

   출력: VIPCustomer의 grade:SILVER
   ```   
   부모 클래스의 생성자에서 선언한 값이 자식 클래스에 그대로 반영이 됩니다.   

1. # 상속시 클래스 실행 순서
   자식 클래스를 실행하면 부모 클래스가 먼저 호출 됩니다.   
   그렇기 때문에 부모 클래스 생성자에서 설정한 값을 자식 클래스에서 사용 가능합니다.   
   ```java
   class Customer{
      public Customer() {
            customerGrade = "SILVER";
            bonusRatio = 0.01;
            
            System.out.println("Customer() 생성자 호출");
      }
   }

   class VIPCustomer extends Customer{
      public VIPCustomer() {
            customerGrade = "VIP";
            bonusRatio = 0.05;
            
            System.out.println("VIPCustomer() 생성자 호출");
      }
   }
   ```   
   main에서 VIPCustomer vip = new VIPCustomer(); 를 호출하면   
   Customer() 생성자 호출
   VIPCustomer() 생성자 호출   
   이 실행됩니다.   
   상속을 받은 경우 소스코드에는 명시되어 있지 않지만
   ```java
      public VIPCustomer() {
            super();  //☜ 컴파일러가 입력
            customerGrade = "VIP";
            bonusRatio = 0.05;
            
            System.out.println("VIPCustomer() 생성자 호출");
      }
   ```   
   super()란 키워드를 입력해 놓습니다.

1. # 상속에서 super()
   부모 클래스를 자식 클래스가 상속받을 때 컴파일러가 자식 클래스에 super()를 암묵적으로 입력을 합니다. 이 super()는 __반드시 자식 생성자 첫 줄__ 에 위치해야 되며 __부모의 기본 생성자__ 를 호출하게 됩니다. 만약 부모 클래스에 기본 생성자가 없다면 에러가 발생합니다.   
   ```java
      class Customer{  // ☜ 부모 클래스
      public Customer(String grade, double rate) {  // ☜ 기본 생성자 아님
            customerGrade = grade;  
            bonusRatio = rate;
            
            System.out.println("Customer() 생성자 호출");
         }
      }

      class VIPCustomer extends Customer{
         public VIPCustomer() {
               super(); // ☜ error 발생
               customerGrade = "VIP";
               bonusRatio = 0.05;
               
               System.out.println("VIPCustomer() 생성자 호출");
         }
      }
   ```   

   이런 경우 보통 VIPCustomer에서 값을 입력 받습니다.   
   ```java
      class VIPCustomer extends Customer{
         public VIPCustomer(String grade, double rate) {
               super(grade, rate); // ☜ super로 인수를 넘김
               customerGrade = "VIP";
               bonusRatio = 0.05;
               
               System.out.println("VIPCustomer() 생성자 호출");
         }
      }
   ```   

   super() 이용해서 부모 클래스 값에 접근 할 수 있습니다.
   ```java
      super.bonusPoint;
      super.name;
      super.id;
   ```   
   super.bonusPoint와 super.name과 super.id는 부모 클래스에 존재하는 값들입니다.   


1. # 부모 변수와 메소드에 접근 방법



1. # 메소드 기능이 약간 다른 경우 