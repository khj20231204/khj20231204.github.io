---
layout: single
title: Object클래스_equals
categories: JAVA
tag: [object,equals, toString]
---

1. # Object클래스
   Object클래스는 모든 클래스의 최상위 클래스입니다. 아무것도 상속 받지 않으면 자동으로 Object를 상속받기 때문에, Object가 가지고 있는 메소드는 모든 클래스에서 사용할 수 있습니다.   

1. # equals(Object obj)

   Object는 모든 클래스들의 최상위 클래스이기 때문에 매개 타입이 Object로 되어있다는 건 모든 객체가 매개값으로 대입될 수 있다는 것을 뜻합니다. 

   - equals는 객체를 비교하는 메서드입니다.   
   - 비교연산자인 ==과 동일한 결과를 리턴합니다.   
   - 객체의 참조변수를 받아서 __주소값__ 을 비교합니다.   

   ```java
   char[] c1 = {'a','b','c'};
   char[] c2 = {'a','b','c'};
   System.out.println(c1.equals(c2)); //false
   System.out.println(c1 == c2); //false
   ```   
   데이터 값은 'a','b','c'로 동일하지만 c1과 c2의 주소값이 다르기 때문에 false를 리턴합니다.   
   ```java
      public class ObjectApi {
         class A {
         }

         class B extends A {
         }

         public void objectFunc() {
            A a = new A();
            B b = new B();
            System.out.println(b.equals(a)); //false
            A c = b;
            System.out.println(b.equals(c)); //true
         }
      }    
   ```   
   클래스B는 클래스A를 상속받았지만 생성된 주소값이 a와 b가 서로 다르기 때문에 false를 리턴합니다.   
   변수 c는 선언은 클래스A로 선언했지만, 대입된 객체의 주소값이 b이기 때문에 true를 리턴합니다.   

1. # equals override
   재정의하지 않은 equals메서드는 == 연산자와 같이 해당 값들의 주소값을 비교하기 때문에 일반적으로 해당 값들이 가지고 있는 "값"을 비교하도록 재정의하여 사용합니다.   

   *자주 사용하는 String클래스는 equals 메소드가 값들을 비교하도록 이미 재정의 되어있습니다.   

   ```java
      public class A {

         private String name;

         public A(String name){
            this.name = name;
         }

         @Override
         public boolean equals(Object obj) {
            if(obj instanceof A){
                  if(this.name.equals(((A) obj).name)){
                     return true;
                  }
            }
            return false;
         }
      }  

      A oe = new A("abcd");
      A oe1 = new A("abcd");
      System.out.println(oe.equals(oe1));
      //출력: true
   ```   
   오버라이딩 하지 않았다면 oe와 oe1이 각각 다른 주소값을 가지고 있기 때문에 false가 나올 것입니다. name이 String으로 선언되어있고 String의 equals가 이미 값을 비교하는 메소드로 재정의 되어있기 때문에   
   if(this.name.equals(((A) obj).name))   
   이와 같은 코드가 가능합니다.   

1. # toString
   1. 객체에 대한 정보를 클래스 이름과 해시코드로 나타냅니다.
   ```java
      ObjectApi oa = new ObjectApi();
      oa.objectFunc();
      System.out.println(oa.toString()); //api_class.ObjectApi@2f4d3709 패키지.클래스이름@해시코드
   ```
   1. String클래스는 String인스턴스가 갖고 있는 문자열을 반환하도록 오버라이딩되었습니다.
   ```java
      String str = new String("abcd");
      System.out.println(str.toString()); //abcd
   ```
   1. Date클래스는 날짜와 시간을 반환하도록 오버라이딩되었습니다.
   ```java
      Date date = new Date();
      System.out.println(date.toString()); //Mon Jun 26 23:15:06 KST 2023
   ```
   1. 보통 toString()메서드는 바로 사용하지 않고 <span style="color:red"> __override__ 를 해서 사용한다.</span>

   
   

  