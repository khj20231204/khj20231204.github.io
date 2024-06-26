---
layout: single
title: 인터페이스 사용 이유와 다형성
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
    
   또는 A클래스가 interface_1과 interface_2와 interface_3을 다중상속 받은 경우   
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

1. # 메소드에서 사용
   __*선언은 인터페이스, 실제 사용에서 넘겨 줄 땐 구현 클래스의 인스턴스__  

   1) 매개변수로 인터페이스 사용   
   ```java
      public class Television implements RemoteControl{..} //RemoteControl인터페이스를 상속 받은 Television클래스   
      public class Audio implements RemoteControl{ .. } //RemoteControl인터페이스를 상속 받은 Audion클래스

      Main(){
         Television tv = new Television(); //RemoteControl의 구현 클래스인 Television의 인스턴스 tv생성
         Audio audio = new Audio(); //RemoteControl의 구현 클래스인 Audio의 인스턴스 audion생성

         paramInterface(tv); //메소드의 매개변수로 Television의 인스턴스 tv 를 넘김
         paramInterface(audio); //메소드의 매개변수로 Audio의 인스턴스 audio를 넘김

         //또는

         paramInterface(new Television()); //메소드의 매개변수로 구현 클래스 Television을 바로 넘김
         paramInterface(new Audio()); //메소드의 매개변수로 구현 클래스 Audio를 바로 넘김
      }

      public void paramInterface(RemoteControl rc){ .. } //RemoteControl를 매개변수로 받는 메소드 정의
   ```  
   메소드의 매개변수로 인터페이스를 선언하면 실제 사용 시 이 인터페이스를 상속받아 구현된 구현 클래스의 인스턴스를 넘겨주면 됩니다. 그럼 다형성에 의해 하나의 메소드에 다양한 인스턴스를 넘겨주는 것이 가능합니다.   

   2) 리턴 값으로 인터페이스 사용    
   ```java
      public class Television implements RemoteControl{..}
      public class Audio implements RemoteControl{ .. }

      Main(){
         returnInterface();
      }

      public RemoteControl returnInterface(){ //리턴 타입으로 RemoteControl 인터페이스를 사용
        Television tv = new Television();
        Audio audio = new Audio();

        return tv; 또는 audio; //리턴 값으로 구현 객체의 인스턴스를 넘겨주게 됩니다.

        //또는

        return new Television(); 또는 new Audio();
      }
   ```   
   리턴 타입 값이 RemoteControl이기 때문에 다형성에 의해 반환 값으로 tv와 audio 모두 반환하는 것이 가능합니다.   

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
   인터페이스로 기능 함수 설계   
   상속 받은 클래스에선 함수 내용 설계

   예)도서관에 책을 반납하는 선반이 있는데 책을 먼저 꽂은 순서대로 먼저 처리가 되는 선반이 있다.   
   인터페이스(Queue) - 책 입력 함수, 처리 후 책 삭제 함수, 현재 처리할 남은 책 수   
   클래스(Shelf) - 책 입력받을 기능 구현, 삭제할 기능 구현, 남은 책 권수 리턴 기능 구현   
   
   클래스와 인터페이스를 상속 받을 BookShelf클래스 설계

   ```java
      //Queue 인터페이스
      public interface Queue {
         void enQueue(String title);  //책을 입력받음
         String deQueue();  //책을 처리함
         int getSize();  //현재 남은 책 수
      }

      //Shelf 클래스
      public class Shelf {

         private ArrayList<String> shelf;

         public Shelf(){
            shelf = new ArrayList<String>(); 
         }

         public void addShelf(String title){  //책 추가
            shelf.add(title);
         }

         public String deleteShelf(){  //책 반납처리(삭제)
            String str = "";

            if(shelf.size()>0)
               str = shelf.remove(0);

            return str;
         }

         public int getCount(){  //남은 책 수
               return shelf.size();
         }
      }

      //Queue인터페이스와 Shelf클래스를 상속받는 BookShelf클래스
      public class BookShelf extends Shelf implements Queue{
         @Override
         public void enQueue(String title) {  //함수는 인터페이스
            addShelf(title);  //기능은 상속받은 클래스
         }

         @Override
         public String deQueue() {  //함수는 인터페이스
            return deleteShelf();  //기능은 상속받은 클래스
         } 

         @Override
         public int getSize() {  //함수는 인터페이스
            return getCount();  //기능은 상속받은 클래스
         }
      }

      //Main
      public static void main(String[] args){
         Queue bookQueue = new BookShelf();

         bookQueue.enQueue("magician of oz 1");
         bookQueue.enQueue("magician of oz 2");
       
         System.out.println(bookQueue.getSize());  //2

         System.out.println(bookQueue.deQueue());  //magician of oz 1
         System.out.println(bookQueue.deQueue());  //magician of oz 2
         System.out.println(bookQueue.deQueue());  //""

         System.out.println(bookQueue.getSize());  //0
      }
   ```
   