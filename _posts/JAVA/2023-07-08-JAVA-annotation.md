---
layout: single
title: 어노테이션(Annotation)
categories: JAVA
tag: [어노테이션]
---

1. # 표준 어노테이션   
   @Override  
   컴파일러에게 오버라이딩하는 메서드라는 것을 알린다.   
   @Deprecated   
   앞으로 사용하지 않을 것을 권장하는 대상에 붙인다.   
   @SuppressWarnings   
   컴파일러의 특정 경고메시지가 나타나지 않게 해준다.   
   @FunctionalInterface   
   함수형 인터페이스라는 것을 알린다.   

1. # 메타 어노테이션
   @Target   
   어노테이션이 적용가능한 대상을 지정하는데 사용한다.   
   @Documented   
   어노테이션 정보가 javadoc으로 작성된 문서에 포함되게 한다.   
   @Inherited   
   어노테이션이 자손 클래스에 상속되도록 한다.   
   @Retention   
   어노테이션이 유지되는 범위를 지정하는데 사용한다.   
   @Repeatable   
   어노테이션이 반복해서 적용할 수 있게 한다.   
   
>자바의정석 교재 정리   

