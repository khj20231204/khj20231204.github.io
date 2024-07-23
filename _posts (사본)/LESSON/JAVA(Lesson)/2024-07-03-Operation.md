---
layout: single
title: 07_03.연산자(lesson)
categories: JAVA(Lesson)
tag: []
---

1. # "=="과 equals
   `>=`나 `>=` 는 부등호 먼저 오고 등호가 옵니다.   

   ```
      String str1 = "자바";
      String str2 = "자바";
      String str3 = new String("자바");
   ```  
   "자바"라는 문자열은 참조형으로 heap이란 공간에 1개만 생성됩니다. str1이 "자바"이고 str2가 "자바"라고해서 따로 생성되는 것이 아니라 heap영역에 "자바"라는 문자열은 1개만 생성됩니다.   
   new연산자를 이용해서 생성시 새로운 heap영역에 "자바"가 생성됩니다.   

   ```
      if(str1 == str2)
   ```   
   는 true를 반환하게 됩니다. "=="연산자는 주소값을 비교하게 되는데 같은 주소를 참조하고 있기 때문입니다.   

   ```
      if(str1 == str3)
   ```   
   는 str1과 str3가 서로 다른 주소를 가지기 때문에 false를 반환하게 됩니다.   

   ```
      str1.equals(str2);
      str1.equals(str3);
   ```   
   equals는 값을 비교하기 때문에 str1 = str2 = str3 이 전부 같은 true를 반환하게 됩니다.   

   __참조형 : 배열, 클래스, 인터페이스__

   java.io (BufferedReader, FileReader, FileWrier, File)

   Scanner는 java.util에 존재
   ```
      Scanner sc = new Scanner(System.in);

      int n1 = sc.nextInt();
      int n2 = sc.nextInt();
   ```   
   입력시 n1과 n2는 스페이스바 또는 엔터로 구분.   

   ```
      avg = tot / 5;
   ```   
   tot인 총합을 숫자 5로 나눠서 평균을 구할 때 tot와 5가 둘 다 int형이기 때문에 결과값이 int로 나옵니다. 소수점으로 나오게 하기 위해서 double형으로 바꿔야 하는데
   이때, tot나 5를 double로 강제 형변환하거나, 5를 5.0으로 변경합니다.   
   ```
      avg = (double)tot / 5;
      avg = tot / (double)5;
      avg = tot / 5.0;
   ```   
   다음과 같이 3가지로 해결할 수 있습니다.

   __1.int형과 int형을 산술연산을 수행하면 int형으로 처리됩니다.__   
   __2.int형과 double형을 산술연산을 수행하면 큰자료형인 double형으로 처리됩니다.__   

1. # Math 
   Math클래스는 모든 필드와 메소드들이 static으로 되어 있습니다. 그렇기 때문에 생성자 없이 바로 .으로 모든 필드와 메소드에 접근할 수 있습니다.   
   그렇기 때문에 new연산자로 생성을 할 수 없습니다.
   ```
      Math math = new Math(); //오류 발생
   ```   

   random() 메소드 설명
   ```
      Returns a double value with a positive sign, greater than or equal to 0.0 and less than 1.0.   
      double형의 양수만 출력하고, 0.0은 포함해서 더 큰수와 1.0은 포함하지 않으며 더 작은 수를 리턴합니다.
   ```   
   
