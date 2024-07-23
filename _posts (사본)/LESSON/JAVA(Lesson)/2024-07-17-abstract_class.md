---
layout: single
title: 07_17.추상 클래스
categories: JAVA(Lesson)
tag: []
author_profile: false
---

1. # 추상 클래스(공통 코드)
   클래스를 설계도에 비유한다면, 추상 클래스는 미완성 설계도에 비유할 수 있습니다. 그 이유는 미완성 메소드(추상 메소드)를 포함하고 있기 때문입니다. 'abstract'로 선언된 추상메소드는 상속받은 자식 클래스에서 반드시 재정의해줘야 합니다.   
   추상 클래스는 추상 메소드를 포함하고 있다는 것외에는 일반 클래스와 다른점이 없습니다. 추상 클래스에서도 생성자, 멤버변수, 메소드 등 모든 것을 가질 수 있습니다. 단만 여기에 추상 메소드를 포함하는 점이 일반 클래스와 다를 뿐입니다.    
   추상 클래스는 추상 메소드를 포함할 수도 있다는 것이지 필수로 포함해야 한다는 것은 아닙니다. 추상 클래스가 되는 조건은 추상 메소드의 포함 유무가 아니라 class 앞에 'abstract'의 유무로 판별됩니다. 그렇기 때문에 추상 메소드를 포함하고 있지 않은 클래스에도 'abstract'를 붙여서 추상 클래스로 지정할 수 있습니다. 추상 메소드가 없는 완성된 클래스라도 추상 클래스로 지정되면 인스턴스를 생성할 수 없습니다.    

   공통 코드 - 필드, 메소드   
   추상 클래스는 추상 메소드를 가지고 있으며, 상속 받은 클래스들은 추상 메소드를 필수 오버라이딩 해야 합니다.   

   1)추상 클래스는 자체적으로 객체를 생성할 수 없습니다.   
   ```java
      public abstract class AbsClass{

      }
   ```   

   2)추상 클래스를 구성하는 요소는 필드, 생성자, 메소드, __추상 메소드__   
   *추상 메소드 : 이름만 있고 내용이 없습니다.   
   ```java
      public abstract class AbsClass{
         int a = 10;             //필드
         abstract void Method(); //추상 메소드
         void Method2(){         //일반 메소드

         }
      }
   ```   

   3)추상 클래스를 상속 받을 때는 extends를 이용해서 상속을 받습니다.   

   4)추상 클래스를 상속받은 일반 클래스는 추상 클래스 안에 들어있는 추상 메소드를 반드시 Method Overriding 해야 합니다.   

   5)추상 클래스도 단일 상속만 가능하다(클래스의 다중 상속을 허용하지 않는다)   

1. # 추상 클래스가 추상 클래스를 상속
   미들 클래스에서 오버라이딩하든 마지막 클래스에서 오버라이딩하든 최소 한군데에선 오버라이딩을 해야합니다.      

   미들 클래스에서 오버라이딩을 하는 경우   
   ```JAVA
      abstract class AbstractClass{				//추상 클래스
         abstract void Method01();				//추상 메소드
               void Method02() {						//일반 메소드
                  System.out.println("Method02 : 추상 클래스에서 구현"); 
               }
            }

      abstract class MiddleClass extends AbstractClass{	//추상 클래스가 추상 클래스를 상속받을 때도 extends
         public void Method03() {
            System.out.println("Method03 : 추상 클래스에서 구현");
         }
         @Override
         void Method01() {    //<---------------------------------미들 클래스에서 오버라이딩
            System.out.println("Method01 : 자식 클래스에서 메소드 오버라이딩한 메소드");
         }
      }

      class SubClass extends MiddleClass{

      }

   ```

   최종 클래스에서 오버라이딩을 하는 경우   
   ```java
      abstract class AbstractClass{				//추상 클래스
      abstract void Method01();				   //추상 메소드
            void Method02() {						//일반 메소드
               System.out.println("Method02 : 추상 클래스에서 구현"); 
            }
         }

      abstract class MiddleClass extends AbstractClass{	//추상 클래스가 추상 클래스를 상속받을 때도 extends
         public void Method03() {
            System.out.println("Method03 : 추상 클래스에서 구현");
         }
      }

      class SubClass extends MiddleClass{
         @Override
         void Method01() {  //<----------------------------------------최종 클래스 오버라이딩
            System.out.println("Method01 : 자식 클래스에서 메소드 오버라이딩한 메소드");
         }
      }
   ```

1. # 메소드 오버라이딩(형상화)
   ```java
      abstract class ShapeClass{			//부모 클래스
         abstract void draw();			//추상 메소드
      }

      class Circ extends ShapeClass{		//자식 클래스

         @Override
         public void draw() {			//메소드 오버라이딩
            System.out.println("원을 그린다.");
         }
      }

      class Tria extends ShapeClass{		//자식 클래스	

         @Override
         public void draw() {
            System.out.println("삼각형을 그린다.");
         }
      }

      class React extends ShapeClass{		//자식 클래스

         @Override
         public void draw() {			//메소드 오버라이딩
            System.out.println("사각형을 그린다");
         }
      }

      public class AbstractTest04 {

         public static void main(String[] args) {
            ShapeClass c = new Circ();		//업캐스팅 - 자동형변환
            ShapeClass t = new Tria();		//업캐스팅 - 자동형변환
            ShapeClass r = new React();		//업캐스팅 - 자동형변환
            
            c.draw();
            t.draw();
            r.draw();
            }
      }
   ```
