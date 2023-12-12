---
layout: single
title: 람다식
categories: JAVA
tag: [lamda,익명클래스,함수형인터페이스]
---

1. # 람다식이란?
   Java 8 이전 버전에선 함수를 매개변수로 넘기기 위해서 객체를 생성 후에 매개변수에 함수를 넣어야 했습니다.
   ```java
      new Thread(new Runnable() {
             @Override
             public void run() {
                 System.out.println("run exec");
             }
         }).start();
   ```
   Thread의 매개변수로 run()이란 함수를 넣고 싶으면 객체를 생성(new Runnable()) 후 run() 메서드를 매개변수 값으로 넣을 수 있었습니다.   
   이런 불편함을 없애기 위해 메서드를 하나의 식으로 표현한 람다식이 나타나게 되었습니다.   
   람다식은 메서드의 이름과 반환 값을 없애고 (매개변수) -> { 실행문 } 이렇게 표현됩니다.   
   메서드의 이름과 반환 값이 없어지므로 '익명 함수'라고 합니다.   
   람다식의 등장으로 인해 이후 메서드를 변수처럼 다룰 수 있게 된 것입니다.   
   ```java
      //함수
      int op(int a){
         return a*6;
      }

      //람다식
      a -> a*6
   ```   
   매개변수가 1개 일 땐 ()를 생략할 수 있습니다. 문장의 끝에 ;를 사용하지 않습니다.   
   ```java   
      //함수
      int max(int a, int b){
         return a>b ? a : b;
      }

      //람다식
      (a,b) -> a>b ? a : b
   ```   
   return을 사용하면 { }로 묶고 문장 끝은 ;를 사용합니다.   
   ```java
      //함수
      int roll(){
         return (int)(Math.random() * 6);
      }

      //람다식
      () -> (int)(Math.random() * 6)
      //또는
      () -> { return (int)(Math.random()*6); } 
   ```   
   return을 적어주면 {}와 ; 를 사용해야 합니다.
1. # 익명 클래스
   이름이 없으며 선언과 객체의 생성을 동시에 합니다. 단 한번만 사용할 수 있고 오직 하나의 객체만 생성할 수 있는 일회용 클래스입니다. 익명 클래스는 인터페이스를 구현하는 클래스의 인스턴스를 생성하기 위해 사용됩니다.   
   new 클래스이름(){   
      //선언   
   }   
   또는
   new 구현인터페이스이름(){   
      //구현   
   }      
1. # 함수형 인터페이스
   단 하나의 추상 메서드를 가지는 인터페이스를 말합니다. 
1. # 익명 클래스와 함수형 인터페이스 작성
   #### 1)main에서 인터페이스를 상속받은 클래스를 넘겨주는 소스,
   ```java
      public class CarExam2 {
          public static void main(String[] args){
              List<Car> cars = new ArrayList<>();
              cars.add( new Car("작은차",2,800,3) );
              cars.add( new Car("봉고차",12,1500,8) );
              cars.add( new Car("중간차",5,2200,0) );
              cars.add( new Car("비싼차",5,3500,1) );

              printCar(cars, new CheckCarForBigAndNotExpensive()); //CheckCar인터페이스를 상속받은 클래스를 넘겨준다
          }

          public static void printCar(List<Car> cars, CheckCar tester){ //CheckCar인터페이스를 상속받은 클래스들은 다 받을 수 있다:다형성
              for(Car car : cars){
                  if (tester.test(car)) {
                      System.out.println(car);
                  }
              }
          }

          interface CheckCar{ //인터페이스 정의
              boolean test(Car car);
          }

          //내부클래스를 만들어서 사용합니다.
          static class CheckCarForBigAndNotExpensive implements CheckCar{ //CheckCar인터페이스를 상속받은 클래스 정의
              public boolean test(Car car){
                  return car.capacity >= 4 && car.price < 2500;
              }
          }
      }
   ```
   #### 2)main에서 인터페이스를 바로 구현하는 소스
   ```java
      //인터페이스InterfaceA
      public interface InterfaceA { //함수형 인터페이스
         public abstract String funcA(String name); //메서드 1개
      }

      //인터페이스를 매개변수로 받는 메서드가 있는 클래스A
      public class A {
          String name;
          public A(String name){
              this.name = name;
          }
          public String funcA(InterfaceA a) { //매개변수를 인터페이스로 받는다. 
              String str = a.funcA(this.name); //인터페이스엔 필수로 작성해야 하는 추상 메서드가 있기 때문에 컴파일러가 자동으로 형식을 만들어주게 된다
              return str;
          }
      }

      //main에서 클래스A fucnA메서드의 매개변수 인터페이스를 익명 클래스로 정의
      public static void main(String[] args){
         A a = new A("anonymouse");
         String msg = a.funcA(new InterfaceA() {
            @Override
            public String funcA(String name) {
                return "내 이름은 "+ name +" 입니다";
            }
         });
         System.out.println(msg); //내 이름은 anonymouse 입니다
      }
   ```
   InterfaceA를 추상 메서드가 1개 있는 함수형 인터페이스로 작성 후 클래스A의 메서드에서 매개변수로 InterfaceA를 받습니다. main에서 클래스A의 객체를 생성 후
   funcA메서드를 호출 할 때 바로 익명 클래스로 인터페이스를 구현합니다.
   <img style="border: 3px solid black;border-radius:9px;width:680px;" src="../../imgs/java/anonymousClass.jpg">   