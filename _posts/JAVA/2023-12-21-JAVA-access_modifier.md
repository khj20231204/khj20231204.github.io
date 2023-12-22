---
layout: single
title: 접근제한자
categories: JAVA
tag: []
---

1. # 접근 제한자
   다른 패키지에서 클래스나 생성자, 메소드나 필드 등에 대한 접근을 제한하는 것을 말합니다. 접근 제한자는 pulic, protected, default, private 4가지가 있는데 pulic, protected, private를 명시하지 않으면 default가 적용이 되기 때문에 명시적으로 default를 나타내지는 않습니다.   

   public : 모든 패키지에서 접근 가능   
   protected : 같은 패키지 내에서와 상속 받은 경우 접근 가능   
   default : 같은 패키지 내에서만 접근 가능  
   private : 오로지 자신 클래스 내부에서만 접근 가능   

1. # 클래스   
   __default__, __private__ 접근 제한자를 가집니다.   
   ```java
      class A{  //defult 접근 제한자를 가집니다
         ...
      }

      private class A{  //private 접근 제한자
         ...
      }
   ```   

1. # 생성자   
   
   ```java
      //------------------ A패키지 ------------------
      A패키지
      public class Parents {

         Parents(){  //default
            System.out.println("parents defalut");
         }

         public Parents(int i){  //public
            System.out.println("parents public");
         }

         protected Parents(String str){  //protected
            System.out.println("parents protected");
         }

         private Parents(int i, String str){  //private
            System.out.println("parents private");
         }
      }

      //------------------ B패키지 ------------------
      B패키지
      class Child extends Parents {

         Child(){
            //super();  ☜ 부모생성자 - default ,error 발생 
         }

         Child(int i) {
            super(i);  // 부모생성자 - public
         }

         Child(String str){
            super(str);  // 부모생성자 - protected
         }

         Child(int i, String str){
            //super(i, str);  ☜ 부모생성자 - private ,error 발생 
         }
      }
   ```   
   *클래스에서 생성자를 선언하지 않으면 컴파일러에 의해 자동으로 기본 생성자가 추가되는데 이때, __기본 생성자는 클래스의 접근 제한과 동일__ 합니다.   

1. # 필드와 메소드   
   필드와 메소드를 정의할 때 클래스 내부에서만 사용할 것인지, 패키지 내에서만 사용할 것인지, 아니면 다른 패키지에서도 사용할 것인지 결정해야합니다.   
   생성자와 마찬가지로 __public__, __protected__, __default__, __private__ 접근 제한자를 가집니다.   

   public   
   모든 패키지에서 사용 가능합니다.   

   protected   
   같은 패키지 내에서와 상속 받은 경우 사용가능합니다.   

   default   
   접근 제한자를 생략하면 적용되며 같은 패키지 내에서만 사용 가능합니다.   

   private   
   같은 패키지이건 다른 패키지이건 사용 불가능하며 오직 자신 클래스 내에서만 사용가능 합니다.   

   ```java
   //Parents 클래스
      public class Parents {

         public int public_var = 1;
         protected  int protected_var = 2;
         int default_var = 3;
         private int private_var = 4;

         public void public_method() {
            System.out.println("parents public_method");
         }
         
         protected  void protected_method(){
            System.out.println("parents protected_method");
         }

         void default_method(){
            System.out.println("parents default_method");
         }

         private void private_method(){
            System.out.println("parents private_method");
         }
      }

   //Child 클래스
      class Child extends Parents{

         Child(){
            int p1 = this.public_var;
            int p2 = this.protected_var;
            int p3 = this.default_var;  // ☜ error
            int p4 =- this.private_var;  //☜ error

            this.public_method();
            this.protected_method();
            this.default_method();  // ☜ error
            this.private_method();  // ☜ error
         }
      }
   ```

