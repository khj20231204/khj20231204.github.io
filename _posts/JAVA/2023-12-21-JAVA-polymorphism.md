---
layout: single
title: 타입 변환과 다형성
categories: JAVA
tag: []
---

1. # 자동 타입 변환
   상속 관계에 있는 클래스 사이에서 클래스 변환이 일어나는데, 자식은 부모 타입으로 자동 타입 변환이 발생합니다. 자동 타입 변환은 프로그램 실행 도중에 자동으로 타입 변환이 일어나는 것을 말합니다.   
   → 자식은 부모의 특징과 기능을 상속 받기 때문에 부모와 동일하게 취급될 수 있다.  

   ```java
      부모타입 변수 = 자식타입
   ```
   기본 형태는 이렇습니다.

   ```java
      class Parents {

      }

      class Child extends Parents {

      }
   ```   
   Child는 Parents를 상속 받았기 때문에   
   Child c = new Child();   
   Parent p = c;   
   이것이 가능합니다.   

   이 경우 p는 c에서 선언된 필드와 메소드는 사용할 수 없고, 기존 p에 정의된 변수와 메소드만 사용 가능합니다.   
   부모 타입으로 자동 변환된 이후로는 부모 클래스에 선언된 필드와 메소드만 사용할 수 있습니다. 만약 메소드가 __자식 클래스에서 재정의 되었다면 자식 클래스의 메소드가 대신 호출__ 됩니다.

1. # 다형성
   자동 타입 변환을 이용하여 필드나 매개변수에 부모를 상속 받은 자식 객체를 대입하여 다양한 값들의 변형을 구할 수 있는데 이를 다형성이라 합니다.    
   필드 타입을 부모 타입으로 선언하면 다양한 자식 객체들이 저장될 수 있습니다. - 필드의 다형성   
   메소드의 매개 변수에 자식 객체를 지정할 수 있습니다. - 매개변수의 다형성      
   자식 클래스에서 메소드를 오버라이딩 하면 부모 타입에서 메소드를 호출했을 때 오버라이딩된 자식 메소드가 호출이 되기 때문에 다양성과 확장성이 높아지게 됩니다.   
   
   예를 들어 기존 A클래스를 만들고 A클래스만으로 작성된 PolyMain이란 클래스를 만듭니다.   
   이후 업데이트가 되면서 B클래스를 만들었을 경우 PolyMain클래스를 수정하지 않고 다형성을 이용하여 PolyMain클래스에서 B클래스에 해당하는 값들을 호출 할 수 있습니다.   
   A클래스 → PolyMain클래스에서 A클래스 사용 → main에서 PolyMain으로 코드 작성   
   → A클래스를 상속받아 메소드를 재정의한 B클래스 생성 → main에서 PolyMain을 호출할 때 B클래스의 객체를 적용 → __기존 PolyMain클래스의 소스를 변경하지 않고__ 원하는 결과 출력
   ```java
      //A 클래스
      public class A {
         public A(){}

         public void A_Func(){
            System.out.println("A Func");
         }
      }

      //A클래스만을 이용해 PolyMain클래스를 작성
      public class PolyMain {
         A a_obj = new A();  //A class

         public void check(A a){ //Parameter is A
            a.A_Func();
         }  
      }
      ```
      여기까지가 기존에 만들어져있던 코드라 가정하고, 이후 A클래스를 상속한 B클래스를 만들면서 기존 PolyMain 소스를 변경하지 않고, B클래스 값들을 호출 합니다.
      ```java
      //B 클래스
      public class B extends A{  //A를 상속 받음
         public B(){
            //System.out.println("class B construct");
         }

         @Override
         public void A_Func() {  //overriding
            System.out.println("A Func in Class B");
         }

         public void B_Func(){  //new make
            System.out.println("B Func");
         }
      }      
   ```   
   B클래스를 새로 만들었습니다.   

   main에서 호출   
   ```java
      public static void main(String[] args){
        //--------------- 기존 A class
        PolyMain pm = new PolyMain();
        pm.a_obj.A_Func();

        pm.check(new A());


        //-------------- 추가된 B class
        B b = new B();
        pm.a_obj = b;  //a객체에 b객체 대입 - 필드의 다형성
        pm.a_obj.A_Func();  //A Func in Class B, b객체의 메소드가 대신 호출

        pm.check(b);  //A Func in Class B - 매개 변수의 다형성

        B b_typeCh = (B)b;  //강제 타입 변환
        b_typeCh.B_Func();  //B Func, B클래스에 있는 메소드 사용 가능
    }
   ```

1. # 강제 타입 변환
   부모 타입을 자식 타입으로 변환하는 것을 말합니다. 자식 타입이 부모 타입으로 자동 변환된 후 다시 자식 타입으로 변환할 때 강제 타입 변환을 사용할 수 있습니다.   
   ```java
      Parent p = new Child();  //자동 변환
      Child c = (Child)p;  //강제 타입 변환
   ```   
   자동 변환이 된 경우 자식에서 선언된 필드와 메소드는 변수p에서 사용할 수 없습니다.    
   강제 타입으로 한번 더 변환을 해주게 되면 자식에서 선언된 필드와 메소드를 사용할 수 있습니다.   
   강제 타입 변환은 자식 타입이 부모 타입으로 변환되어 있는 경우만 가능합니다.   

1. # 객체 타입 확인
   강제타입 변환을 하기 위해선 자식 타입이 부모 타입으로 변환되어 있어야 하기 때문에 처음부터 부모 타입으로 생성된 객체는 변환 할 수 없습니다.   
   따라서 해당 변수가 자식 클래스의 인스턴스인지 먼저 확인을 해야 합니다.   
   ```java
      boolean result = obj(객체) instanceof type(타입);
   ```   
   instance of 연산자는 obj가 해당 type인지를 검사하게 됩니다.   

   위에 해당 코드를
   ```java
      B b_typeCh = (B)b;  //강제 타입 변환
   ```   

   아래와 같이 체크를 해야 합니다.   
   ```java
      if(b_typeCh instanceof B) {
         B b_typeCh = (B)b;  //강제 타입 변환
      }
   ```
