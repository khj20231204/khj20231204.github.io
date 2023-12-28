---
layout: single
title: Generic
categories: JAVA
tag: []
---
 
1. # Generic
   클래스 내에 다양한 필드와 메소드가 존재하는데 필드와 메소드의 기능은 동일하지만 타입만 바꿔서 사용해야하는 경우가 있습니다. 예를 들면 프린터기에 카트리지 종류를 잉크로 하는 경우와 토너로 해야하는 경우 프린터기의 기능은 같지만 장착하는 재료만 다른 경우, 클래스를 새로 만들 수도 있지만 그렇게 되면 메모리낭비와 오버스택이 발생할 수 있습니다. 제네릭은 하나의 클래스에 여러 타입을 받아들일 수 있는 기능을 제공합니다.   
   자바 v.5 이전에는 모든 클래스의 최상위 클래스인 Object를 이용하여 이러한 기능을 수행했는데, 타입을 변형 할 때마다 타입체크와 형변환을 해줘야 했습니다. 제네릭은 이런 불편함을 없애고 타입 안전성을 제공합니다.    

   ```java
      class A<T> {

         T material;

         public void setMaterial(T material){
            this.material = matiarial;
         }
      }
   ```
   

1. # 예제
   잉크 클래스와 토너 클래스는 재료의 명칭만 다를 뿐 동일한 역할을 한다고 예를 들겠습니다.   
   잉크 클래스 생성 - 토너 클래스 생성 - 일반적인 Generic 클래스 생성
   ```java
      //잉크 클래스
      public class ThreeDPrintInk {
         private Ink material;

         public ThreeDPrintInk(Ink material){
            this.material = material;
         }

         public Ink getMaterial() {
            return material;
         }

         public void setMaterial(Ink material) {
            this.material = material;
         }

         public String toString(){
            return material.toString();
         }
      }

      //토너 클래스
      public class ThreeDPrintToner {
         private Toner material;

         public ThreeDPrintToner(Toner material){
            this.material = material;
         }

         public Toner getMaterial() {
            return material;
         }

         public void setMaterial(Toner material) {
            this.material = material;
         }

         public String toString(){
            return material.toString();
         }
      }
      ```   
      밑에는 위에 2개의 클래스를 일반화한 제네릭 클래스입니다. Ink와 Toner가 들어갈 값에 임의의 타입 변수 'T'를 입력합니다.
      ```java
      //Generic 클래스
      public class ThreeDPrintGeneric<T>{

         private T material;

         public ThreeDPrintGeneric(T material){
            this.material = material;
         }

         public T getMaterial() {
            return material;
         }

         public void setMaterial(T material) {
            this.material = material;
         }

         public String toString(){
            return material.toString();
         }
      }
   ```   
   제네릭 클래스 호출   
   ```java
      ThreeDPrintGeneric<Ink> genericInk = new ThreeDPrintGeneric<>(ink);
      System.out.println("Generic ink : " + genericInk.toString());

      ThreeDPrintGeneric<Toner> genericToner = new ThreeDPrintGeneric<>(toner);
      System.out.println("Gneric toner : "+ genericToner.toString());
   ```   
   ThreeDPrintGeneric<Ink> genericInk = new ThreeDPrintGeneric<>(ink)
   클래스명<대입될 타입> 변수명 = new 클래스명<>(생성자 입력 값)   
   <> : 다이아몬드 연산자라고 합니다. 좌변엔 대입될 타입을 입력하고 우변엔 예전에 똑같이 대입될 타입을 입력했었는데, 요즘은 빈칸으로 놓습니다.    
   () : 우변 마지막 () 안에는 생성자에 대입할 초기화 데이터를 입력합니다.   
