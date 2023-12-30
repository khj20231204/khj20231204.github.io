---
layout: single
title: Generic
categories: JAVA
tag: []
---
 
1. # Generic
   클래스 내에 다양한 필드와 메소드가 존재하는데 필드와 메소드의 기능은 동일하지만 타입만 바꿔서 사용해야하는 경우가 있습니다. 예를 들면 프린터기에 카트리지 종류를 잉크로 하는 경우와 토너로 해야하는 경우 프린터기의 기능은 같지만 장착하는 재료만 다른 경우, 클래스를 새로 만들 수도 있지만 그렇게 되면 메모리낭비와 오버스택이 발생할 수 있습니다. 제네릭은 하나의 클래스에 여러 타입을 받아들일 수 있는 기능을 제공합니다.   
   자바 v.5 이전에는 모든 클래스의 최상위 클래스인 Object를 이용하여 이러한 기능을 수행했는데, 타입을 변형 할 때마다 타입체크와 형변환을 해줘야했습니다. 제네릭은 이런 불편함을 없애고 타입 안전성을 제공합니다.    

   ```java
      public class GenericTypeVal <A,B,C> { //class 필드와 생성자에서 사용되는 타입변수 A,B,C 선언
         A a;
         B b;
         C c;

         public GenericTypeVal(A a, B b){  //생성자에서 A, B 타입변수 입력
            this.a = a;
            this.b = b;
         }

         public void setC(C c){
            this.c = c;
         }

         public C getC(){
            return c;
         }

         public static <R> void func(R r){  //generic class와 generic method는 서로 관여를 하지 않습니다. 메소드에서 사용되는 새로운 타입변수 <R> 선언
            System.out.println("Generic Type - Static Method :"+ r);
         }

         public <Q> void func2(Q q){}  ////generic class와 generic method는 서로 관여를 하지 않습니다.

         public String toString(){
            return "a="+ a.toString() + " , b=" + b.toString();
         }
      }
   ```   
   입력받을 타입을 <> 다이아몬드 연산자 안에 갯수 만큼 써주고   
   필드와 생성자에서 사용할 땐   
   GenericTypeVal <A,B,C>  ☜ 클래스 옆   
   메소드로 사용할 땐   
   public static <R> void func(R r) ☜ 메소드 반환 타입 옆   
   public <Q> void func2(Q q) ☜ 메소드 반환 타입 옆   
   각각 선언해 주고, 이후엔 일반적으로 사용하는 타입 방식과 같습니다.   

   <> 연산자 안에는 참조 타입이 와야합니다. 따라서 int, short, double 대신 Interger, Short, Double 래퍼클래스가 와야합니다.

   ```java
      ppublic static void main(String[] args){
        GenericTypeVal<Long, Double, String> gtv = new GenericTypeVal<>(11l,22d);
        //선언 시 클래스에서 사용할 <Long, Double, String> 로 <A,B,C> 타입 설정 , 초기화는 (11l,22d) A,B 타입만 해당
        System.out.println(gtv.toString()); //a=11 , b=22.0

        gtv.setC("type String");
        System.out.println(gtv.getC()); //type String

        GenericTypeVal.func("anonymous"); //Generic Type - Static Method :anonymous
        GenericTypeVal.func(345); //Generic Type - Static Method :345
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

1. # <T extends 클래스>   
   타입 변수 T에 모든 타입이 올 수 있지만, extends를 사용하게 되면 클래스를 상속받은 자손만 타입으로 올 수 있습니다. T 자료형의 범위를 제한하기 위해서 "extends 클래스"를 사용하게 됩니다.   

   ```java
      //Material 클래스
      public class Material {
         ...
      }

      //Ink 클래스
      public class Ink extends Material{
         ...
      }

      //Toner 클래스
      public class Toner extends Material {
         ...
      }

      public class ThreeDPrintGeneric<T extends Material>{  // ☜ Material을 상속받은 자식 타입만 T에 올 수 있습니다.
         ...
      }
   ```   
   ThreeDPrintGeneric<Ink> pInk = new ThreeDPrintGeneric<>();   
   ThreeDPrintGeneric<Toner> pInk = new ThreeDPrintGeneric<>();   
   와 같이 Material의 자식만 T타입에 올 수 있습니다.   
   
1. # Generic 메소드
   제네릭을 사용하는 메소드는 클래스가 제네릭이든 아니든 상관없이 독립적으로 사용할 수 있습니다.   

   x,y를 제네릭타입으로 가지는 Point의 두 점을 가지고 사각형을 만들어 넓이는 구하는 예제입니다. x, y 두 변수를 매개타입으로 입력을 받습니다.      
   ```java

      //Point 클래스
      public class Point <T,V>{

         T x;
         V y;

         public Point(T x, V y){
            this.x = x;
            this.y = y;
         }

         public T getX(){
            return x;
         }

         public V getY(){
            return y;
         }
      }

      
      public class GenericMethod {  //GenericMethod 클래스는 일반 클래스
         public <T,V> double makeRectangle(Point<T,V> p1, Point<T,V> p2){
         //makeRectangle 넓이구하는 함수는 제네릭 이용
         double left = ((Number) p1.x).doubleValue();  //T
         double right = ((Number) p2.x).doubleValue();  //V
         double top = ((Number) p1.y).doubleValue();  //T
         double bottom = ((Number) p2.y).doubleValue();  //V

         double width = right - left;
         double height = top - bottom;

         return width * height;
         }
      }

      //main
      public static void main(String[] args){
        Point<Integer, Double> p1 = new Point<>(2,8.6);
        Point<Integer, Double> p2 = new Point<>(7,2.3);

        GenericMethod gm = new GenericMethod();
        double result = gm.<Integer, Double>makeRectangle(p1, p2);
        //함수를 호출 시 매개타입 지정
        System.out.println(result);
      }
   ```   
   Point를 Integer와 Double로 입력을 받고 makeRectangle함수에서 전부 double로 형변환을 한 후 넓이를 구하고 이를 반환합니다. 주목해야 할 것은 makeRectangle함수는 제네릭을 사용하는데 GenericMethod클래스는 일반 클래스입니다. 함수에서 제네릭 사용과 클래스는 무관합니다.      