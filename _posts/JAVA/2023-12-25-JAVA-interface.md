---
layout: single
title: 인터페이스 다형성
categories: JAVA
tag: []
---

1. # 인터페이스의 다형성
   개발 코드와 객체가 서로 통신하는 접점 역할을 합니다. 인터페이스를 두므로써 기존 개발 코드를 수정하지 않고 사용하고 있는 개체를 변경할 수 있습니다.   

   ```java
      interface명 변수 = new 클래스명
   ```
   해당 interface를 implements한 클래스라면 위와 같이 클래스를 인터페이스 타입에 할당하는 것이 가능합니다.   
   이 경우,
   ```java
      interface명 변수 = new A클래스();
      interface명 변수 = new B클래스();
      interface명 변수 = new C클래스();
      ...
   ```   
   기존 코드는 변경하지 않고 새로 생성된 A,B,C클래스를 인터페이스에 할당만 하면 변경된 결과를 얻을 수 있습니다.   
   예를 들면,
   ```java
      UserInfoDao userInfoDao = null;

      if(dbType.equals("ORACLE")){
         userInfoDao = new UserInfoOracleDao();  //☜ UserInfoDao인터페이스에 UserInfoOracleDao클래스 할당
      }else if (dbType.equals("MYSQL")){
         userInfoDao = new UserInfoMySqlDao();  //☜ UserInfoDao인터페이스에 UserInfoMySqlDao클래스 할당 
      }else {
         System.out.println("db error");
         return;
      }

      //활용
      if(userInfoDao != null){
         userInfoDao.insertUserInfo(userInfo);
         userInfoDao.updateUserInfo(userInfo);
         userInfoDao.deleteUserInfo(userInfo);
      }
   ```   
   이런 코드가 가능합니다.   
   userInfoDao란 인터페이스 타입을 생성 후 받는 값에 따라 "UserInfoOracleDao" Oracle을 수행하는 코드를 가진 클래스를 대입할 수 있고, "UserInfoMySqlDao" MySql을 수행하는 코드를 가진 클래스를 대입할 수 있습니다.   
    
   또는
   ```java
      interface_1 변수 = new A클래스();
      interface_2 변수 = new A클래스();
      interface_3 변수 = new A클래스();
      ...
   ```
   다양한 인터페이스를 생성 후 클래스를 할당할 수도 있습니다.   

   예를 들면,
   ```java
      UserBuyInf buyer = new Customer();  //☜ UserBuyInf인터페이스에 Customer클래스 할당
      buyer.buy();
      buyer.order();

      UserSellInf seller = new Customer();  //☜ UserSellInf인터페이스에 Customer클래스 할당
      seller.sell();
      seller.order();
   ```   
   이런 식으로 인터페이스에 클래스를 대입 후 인터페이스에서 제공하는 메소드들 호출할 수 있습니다.   

1. # 인터페이스의 다중 상속
   구현 객체가 있어 상속시 모호성을 가지는 클래스 상속과는 다르게 구현 객체가 없기 때문에 인터페이스는 다중 상속이 가능합니다. 상속시 상수 필드는 인터페이스로 바로 접근을 하게 되고, 추상 메소드는 내부 내용을 기술하여 실체 메소드로 만들고, default 메소드는 부모 인터페이스의 default 메소드를 사용하거나 오버라이딩을 하게 됩니다.   

   Interface : UserBuyInf, UserSellInf → Customer 클래스가 다중 상속
   ```java
      public interface UserBuyInf {

         int LIMIT = 10;  //상수

         void buy();  //추상 메소드

         default void order() {  //default 메소드
         System.out.println("Order to Buy");
         }
      }

      public interface UserSellInf {

         int LIMIT = 20;  //상수
 
         void sell();  //추상 메소드

         default void order(){  //default 메소드
            System.out.println("Order of Sell");
         }
      }
   ```   
   
   UserBuyInf와 UserSellInf 인터페이스 2개를 상속받은 Customer클래스 생성
   ```java
      public class Customer implements UserBuyInf, UserSellInf {  //인터페이스 다중 상속
         @Override
         public void buy() {  //UserBuyInf인터페이스 메소드 오버라이딩
            System.out.println("Buy of Custmoer");
         }

         @Override
         public void sell() {  //UserSellInf인터페이스 메소드 오버라이딩
            System.out.println("Sell of Customer");
         }

         @Override
         public void order() {  //default 메소드 
            UserBuyInf.super.order();  //부모 인터페이스 UserBuyInf의 order메소드 사용
         }

         public void customerInfo(){  //Customer에서 새로 생성한 메소드
            System.out.println("Customer Info");
         }
      }
   ```   

   main에서 Customer클래스 사용
   ```java
      public static void main(String[] args){

         Customer customer = new Customer();
         customer.buy();  //Buy of Custmoer
         customer.sell();  //Sell of Customer
         customer.order();  //Order to Buy
         customer.customerInfo();  //Customer Info

         UserBuyInf buyer = new Customer(); //UserBuyInf 변수에 Customer클래스의 구현 객체 대입
         buyer.buy();  //Buy of Custmoer
         buyer.order();  //Order to Buy

         UserSellInf seller = new Customer(); //UserSellInf 변수에 Customer클래스의 구현 객체 대입
         seller.sell();  //Sell of Customer
         seller.order();  //Order to Buy ☜ order가 default 메소드인데 Customer클래스에서 "UserBuyInf.super.order()" Buy인터페이스 order 호출.
      }
   ```

1. # 클래스 상속과 인터페이스 구현 함께 쓰기
   
   
   
