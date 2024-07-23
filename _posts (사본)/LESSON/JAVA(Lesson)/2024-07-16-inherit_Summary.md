---
layout: single
title: 07_16.상속에서 멤버변수 정의
categories: JAVA(Lesson)
tag: []
author_profile: false
---

1. # 부모 멤번변수를 사용
    부모 멤버변수에 값이 할당되기 때문에 부모 멤버변수를 호출할 경우 할당된 새로운 값을 가져오게 됩니다.

    ```java
      
      class Parent{
         int x;

         public Parent(int x) {
            this.x = x;
         }
         
         void print() {
            System.out.println("parent x:"+x);
         }
      }

      class Child extends Parent{
         Child(int x) {
            super(1);            //<--------------- Parent의 x에 1대입
            this.x = x;          //<--------------- Parent의 x에 x대입, 위에 1값을 덮는다, 부모 멤버변수에 x할당
         }
         
         @Override
         void print() {
            System.out.println("child x:"+x);
         }
      }

      class Family{
         
         void familyMethod(Parent p) {
            p.print();
            System.out.println("family p.x:"+p.x);
         }
      }

      public class SendValues {

         public static void main(String[] args) {
            
            Child c1 = new Child(200);			   //child의 멤버변수와 메소드 호출
            c1.print(); 						      //200
            System.out.println("c1.x:"+c1.x);   //200	
            
            //경우 1)
            Parent p1 = (Parent)c1;				   //Parent의 멤버변수, Child의 메소드 호출
            p1.print();							      //200
            System.out.println("p1.x:"+p1.x);	//200
            
            //경우 2)
            Parent p2 = new Child(200);			//Parent의 멤버변수, Child의 메소드 호출
            p2.print();							      //200
            System.out.println("p2.x:"+p2.x);	//200
            
            System.out.println();
            
            //경우 3) familyMethod의 매개변수로 c1,p1,p2가 대입될 때 Parent로 형변환 됨
            Family f = new Family();			//Parent의 멤버변수, Child의 메소드 호출
            f.familyMethod(c1); 				   //200	   200
            f.familyMethod(p1);              //200	   200
            f.familyMethod(p2);					//200	   200
         }
      }

      결과값
      child x:200
      c1.x:200
      child x:200
      p1.x:200
      child x:200
      p2.x:200

      child x:200
      family p.x:200
      child x:200
      family p.x:200
      child x:200
      family p.x:200
    ```   
    자식의 이 부분에서   
    ```
    Child(int x) {
            super(1);            
            this.x = x; //<- 부모 멤버변수에 x가 대입
         }
   ```
   부모 멤버변수x에 매개변수로 할당받은 새로운 x값이 대입되고,    
   경우 1),2),3) 에서 parent로 형변환이 되었기 때문에 부모 멤버변수를 호출 시 입력받은 새로운 값이 출력됩니다.   


1. # 멤버변수를 새로 선언
  
   
   멤버변수를 새로 선언한 경우   
   ```java
      class Parent{
         int x=1;             //바로 값 대입
                              //<- 기본 생성자 없음
         void print() {
            System.out.println("parent x:"+x);
         }
      }

      class Child extends Parent{
         int x=200;           //<--------------------- 멤버변수 x를 새로 선언
                              //<- 기본 생성자 없음
         @Override
         void print() {
            System.out.println("child x:"+x);
         }
      }

      class Family{
         
         void familyMethod(Parent p) {
            p.print();
            System.out.println("family p.x:"+p.x);
         }
      }

      public class SendValues {

         public static void main(String[] args) {
            
            Child c1 = new Child();				//child의 멤버변수와 메소드 호출
            c1.print(); 						   //200
            System.out.println("c1.x:"+c1.x);//200	
            
            //경우 1)
            Parent p1 = (Parent)c1;				//Parent의 멤버변수, Child의 메소드 호출
            p1.print();							   //200
            System.out.println("p1.x:"+p1.x);//1
            
            //경우 2)
            Parent p2 = new Child();			//Parent의 멤버변수, Child의 메소드 호출
            p2.print();							   //200
            System.out.println("p2.x:"+p2.x);//1
            
            System.out.println();
            
            //경우 3) familyMethod의 매개변수로 c1,p1,p2가 대입될 때 Parent로 형변환 됨
            Family f = new Family();		//Parent의 멤버변수, Child의 메소드 호출
            f.familyMethod(c1); 				//200	1
            f.familyMethod(p1);				//200	1
            f.familyMethod(p2);				//200	1
         }
      }

      결과 값
      child x:200
      c1.x:200
      child x:200
      p1.x:1
      child x:200
      p2.x:1

      child x:200
      family p.x:1
      child x:200
      family p.x:1
      child x:200
      family p.x:1
   ```   
   경우 1),2),3) 전부 Child가 Parent로 형변환이 된 것이기 때문에 같은 방식으로 동작   
   Parent로 형변환이 된 경우 부모의 멤버변수 x값을 가져오게됩니다.


