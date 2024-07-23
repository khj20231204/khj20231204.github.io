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
   Thread의 매개변수로 run()이란 함수를 넣고 싶으면 객체를 생성(new Runnable()) 후 run() 메소드를 매개변수 값으로 넣을 수 있었습니다.   
   이런 불편함을 없애기 위해 메소드를 하나의 식으로 표현한 람다식이 나타나게 되었습니다.   
   람다식은 메소드의 이름과 반환 값을 없애고 (매개변수) -> { 실행문 }으로 표현됩니다.   
   메소드의 이름과 반환 값이 없어지므로 '익명 함수'라고 합니다.   
   람다식의 등장으로 인해 이후 __메소드를 변수처럼__ 다룰 수 있게 된 것입니다.   
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

1. # 함수형 인터페이스와 람다식
   추상 메소드를 하나만 포함하는 함수형 인터페이스 구현   
   ```java
      public interface FunctionalInterface {
         public int methodOfLamda(int a, int b);
      }
   ```   
   methodOfLamda를 1개 만듭니다. 이제부터 이 메소드의 구현이 람다식이 됩니다.
   
   ```java
      public static void main(String[] args) {

         FunctionalInterface fi = new FunctionalInterface() {
               @Override
               public int methodOfLamda(int a, int b) {
                  return a * b;
               }
         };
      }
   ```   
   인터페이스의 핵심은 "추상 메소드 구현"입니다. 일반적으로 다음과 같이
   ```java
      class FunctionalClass implements FuncionalInterface{
         public int methodOfLamda(int a, int b) {
                  return a * b;
         }
      }
   ```
   클래스에서 인터페이스를 implements해서 추상 메소드를 구현할 구현 클래스를 만들게 되지만 바로 구현 객체를 선언하고 추상 메소드를 구현할 수 있습니다.   
   ```java
      FunctionalInterface fi = new FunctionalInterface() { //new 연산자로 구현객체 생성
            public int methodOfLamda(int a, int b) { //추상 메소드 정의
               ...
            }
      };
   ```   
   이때, 함수형 인터페이스의 핵심인 "추상 메소드 구현"이 람다식으로 표현이 됩니다.   
   ```java
      public static void main(String[] args) {

         FunctionalInterface fi = (a,b) -> a*b;
      }
   ```    
   즉,
    <img src="../../imgs/java/interface_obj.png" style="border:3px solid black;border-radius:9px;width:500px">   
    람다식 자체가 구현 객체의 추상 메소드를 구현한 것입니다.   

1. # 함수형 인터페이스와 람다 예2
   Collection의 sort 메소드의 매개변수로 받아오는 Comparator 인터페이스를 new 연산자를 이용해 객체를 바로 생성하면서 compare 추상 메소드를 구현하는 부분을 람다식으로 표현하겠습니다.   

   Comparator의 구현객체를 만들어 compareTo 메소드를 재정의합니다.
   ```java
      List<String> list2 = Arrays.asList("c","a","d","e");
         list2.sort(new Comparator<String>() { // - ①
            @Override
            public int compare(String o1, String o2) { // - ①
               return o1.compareTo(o2) * (-1); // - ①
           }
      });     
      list2.stream().forEach(System.out::println);
      
      list2.sort((o1, o2)-> o1.compareTo(o2));  // - ②
      list2.stream().forEach(System.out::println);
   ```   
   list2.sort( 이 부분 ) 에서 new 연산자로 Comparator를 구현한 부분(①) 이    
   (o1,o2) -> o1.compareTo(o2); 단 한줄로 표현(②) 됩니다.   

1. # 매개변수로 함수형 인터페이스 사용
   함수형 인터페이스는 람다식을 다루기 위한 특별한 인터페이스고 이 인터페이스에 포함된 추상 메소드의 구현이 람다식의 구현입니다. 이렇듯 함수형 인터페이스와 람다식은 밀접한 관계를 가지기 때문에 매개변수로 함수형 인터페이스를 사용하는 건 매개변수로 람다식을 입력받겠다는 뜻이 됩니다. 람다식을 입력받겠다는 건 추상 메소드의 구현 방식을 입력받겠다는 뜻이 됩니다. 결과값이 아니라 메소드 구현 방식이 됩니다.   
   __추상 메소드의 구현 = 람다식__

   함수형 인터페이스 생성   
   ```java
      public interface FunctionalInterface {
         public int methodOfLamda(int a, int b);
      }
   ```   

   main에서 실행
   ```java
      public static void main(String[] str){
         //매개변수로 함수형 인터페이스를 사용
        FunctionalInterface fiPlus = (int a, int b) -> a+b;

        int x = 6, y = 3;

        int result = functionalMethod(fiPlus,x,y); //매개변수로 함수형 인터페이스 참조변수를 할당
        System.out.println("result:"+result);

        result = functionalMethod((int a, int b) -> a - b, x, y); //매개변수로 람다식 할당
        System.out.println("result:"+result);
      }

      static int functionalMethod(FunctionalInterface fi, int x, int y){
         return fi.methodOfLamda(x,y);
      }
   ```   
   functionalMethod(fiPlus,x,y) fiPlus는 함수형인터페이스의 참조변수입니다. fiPlus를 매개변수 값으로 넘겨주는 건 funcionMethod 메소드안에서 실행하게되는 fi.methodOfLamda(x,y)인 __메소드의 정의__ 를 넘겨주는 것이 됩니다. 일반적인 메소드의 매개변수는 값을 받아와서 그것을 이용하는 방식인데, 람다식으로 넘겨받은 매개변수는 메소드 정의가 됩니다. 이 정의를 메소드 안에서 사용하게 됩니다.   
   functionalMethod((int a, int b) -> a - b, x, y) 직접 람다식을 매개변수로 넘겨줄 수도 있습니다.   

1. # 리턴타입으로 함수형 인터페이스 사용
   매개변수와 마찬가지로 __메소드의 정의__ 를 리턴값으로 넘기게 됩니다.   
   ```java
      public static void main(String[] str){
         //리턴값으로 함수형 인터페이스를 사용
        FunctionalInterface fi = returnFI();
        fi.methodOfLamda(9,4);         
      }

      static FunctionalInterface returnFI(){ //☜ 리턴타입이 함수형 인터페이스
         return (int a, int b) -> a-b; //☜ 람다식을 리턴
      }
   ```   
   함수형 인터페이스를 리턴타입으로 선언하고 람다식을 리턴했습니다. FunctionalInterface인 함수형 인터페이스 안에 있는 추상 메소드 methodOfLamda를 람다식으로 정의해서 리턴한 것이 됩니다. __람다식은 추상 메소드의 구현__ 이기 때문입니다.