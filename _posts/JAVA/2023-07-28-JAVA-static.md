---
layout: single
title: static
categories: JAVA
tag: [static, 정적 멤버]
---

1. # 정적멤버란?
   정적이란 "고정된"이란 의미로 클래스에 고정된 멤버로서 객체를 생성하지 않고 사용할 수 있는 필드와 메소들 말합니다. 이들을 각각 정적 필드, 
   정적 메서드라고 합니다.
1. # 선언
   ```java
      public class 클래스{
         static 타입 필드명;

         static 리턴 타입 메소드(매개변수, ...)
      }
   ```
1. # 메모리 로드시기
   클래스 로더가 클래스를 로딩해서 메소드 영역에 적재할 때 메서드 영역에서 정적필드와 정적 메서드를 관리하게 됩니다. 따라서 클래스 로딩이 끝나는 
   시기에 바로 사용할 수 있습니다.
1. # 정적으로 선언 기준
   1. ## 필드
   필드를 선언할 때 인스턴스 필드로 선언할 것인지 정적 필드로 선언할 것인지 판단 기준이 있어야합니다. 객체마다 가지고 있어야할 데이터이면 인스턴스 필드로 선언하고, 객체마다 가지고 있을 필요가 없는 공용 데이터라면 정적 필드로 선언합니다.
   1. ## 메서드
   메소드 내에 인스턴스 필드를 포함하고 있으면 인스턴스 메서드로 선언하고, 인스턴스 필드를 포함하고 있지 않다면 정적 메서드로 선언합니다.
1. # 정적 메서드 선언 시 주의사항
   객체가 없어도 실행된다는 특징 때문에 정적 메서드를 선언할 때는 이들 내부에 인스턴스 필드나 인스턴스 메서드를 사용할 수 없습니다. 메모리에 로드되는 시기가 서로 다르기 때문입니다.   
   __정적 메서드 안에선 정적 필드나 정적 메서드만 사용가능__   
   또한 this키워드도 사용 불가능합니다.
1. # 정적 메서드에서 인스턴스 멤버 사용법
   정적 메서드에서 인스턴스 멤버를 사용해야 한다면 객체를 먼저 생성한고 참조 변수로 접근해야 합니다.
   ```java 
      static void Method(){
         ClassName obj = new ClassName();
         obj.filed = 10;
         obj.method();
      }
   ```