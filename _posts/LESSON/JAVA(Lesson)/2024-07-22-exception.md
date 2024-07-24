---
layout: single
title: 07_22.예외처리
categories: JAVA(Lesson)
tag: []
author_profile: false
---

1. # 예외처리

   예외 : 프로그램이 실행되는 동안에 발생하는 예상하지 못한 에러   

   예외 처리를 하는 이유 : 프로그램을 안전하게 종료를 하기 위해서 사용   

   1.입출력을 처리할 때   
   2.데이터베이스 연동을 처리할 때   

   java.lang.Exception 클래스가 예외처리 클래스 중 최상위 클래스입니다.   

1. # 예외처리 종류
   ArithmeticException : 0으로 나눌 때 발생   
   ArrayIndexOutOfBoundsException : 배열의 범위를 벗어 났을 때 발생   
   NumberFormatException : 숫자 외의 값을 사용할 때 발생   
   NullPointException : 객체를 생성하지 않고 필드나 메소드를 호출할 때 발생   
   IOException : 입출력을 할 때 발생   
   FileNotFoundException : 파일이 없을 때 발생   
   ClassCastException : 자료형 변환이 되지 않을 경우에 발생   
   SQLException : 데이터베이스와 연동할 때 발생   

1. # throws
   메소드를 호출한 곳으로 예외를 떠넘길 때 throws를 사용합니다. throws 키워드 뒤에는 떠넘길 예외 클래스를 쉼표로 구분해서 나열할 수 있습니다.   
   ```
      리턴타입 메소드이름(매개변수, ...) throws 예외클래스1, 예외클래스2, ...{

      }
   ```   
   예외의 종류별로 throws 뒤에 나열하는 것이 일반적이지만, throws Exception만으로 모든 예외를 간단히 떠넘길 수 있습니다. throws 키워드가 붙어 있는 메소드는 반드시 try블록 내에서 호출 되어야 합니다.

   ```java
      public class ThrowsEx1 {

         public void setData(String n) {
            if(n.length() >= 1) {
               String str = n.substring(0,1);
               printData(str);            //<------------------------------------ 2) printData호출, 4)printData를 호출한 1로 예외를 넘김
            }
         }
         
         private void printData(String n) throws NumberFormatException{
            int dan = Integer.parseInt(n);   //<------------------------------------ 3) NumberFormatException예외 발생, 2로 예외를 넘김
            System.out.println(dan + "단");
            System.out.println("---------------");
            for(int i=0 ; i<10 ;i++) {
               System.out.println(dan + "*" + i + "=" + (dan*i));
            }
         }
         
         public static void main(String[] args) {
            ThrowsEx1 t1 = new ThrowsEx1();
            
            try {
               t1.setData("a");	//<------------------------------------ 1) setData호출
               }catch(Exception e) {   //<------------------------------------ 5) 여기서 Exception을 받음
               System.out.println("첫문자가 숫자가 아닙니다");
            }
         }
      }
   ```   
   예외가 발생하면 자신을 호출한 메소드 위치로 이동 후 예외를 처리하게 됩니다.   
   printData에서 예외가 발생 -> printData를 호출한 setData로 예외를 넘김 -> setData를 호출한 main의 t1.setData가 예외를 받음 -> main의 try catch가 예외를 처리   


