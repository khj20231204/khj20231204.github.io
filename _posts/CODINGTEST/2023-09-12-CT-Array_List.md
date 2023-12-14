---
layout: single
title: array와 list
categories: CODINGTEST
tag: [array, list]
---

1. # 배열
   1) 여러개의 데이터를 한꺼번에 다룰 때 사용합니다.   
   2) Array는 Object는 아니지만 Referece Value로 취급됩니다.   
   3) 메모리상에 연달아 공간을 확보합니다.   
   4) 미리 공간을 확보해 놓고 써야 합니다.   
   5) 한 번 만들어진 공간은 크기가 고정됩니다.   
   6) 값은 index로 접근합니다.   

1. # 배열 선언과 초기화
   ```java
      //선언과 생성
      int[] arr; //배열 선언(배열을 다루기 위한 참조 변수 arr선언)        
      arr = new int[5]; //배열 생성(실제 저장 공간을 생성)
      int[] arr2 = new int[5];


      //선언 시 초기화
      int[] arr4 = new int[]{1,2,3,4,5};E8F5FF
      //int[] arr4 = new int[5]{1,2,3,4,5}; 선언 시 초기화 할 땐 배열크기를 명시하면 error

      int[] arr3 = {1,2,3,4,5}; //바로 초기화 시 new int[] 생략가능

      String[] str = new String[]{"a","b","c"};
      //String[] str = new String[3]{"a","b","c"}; 선언 시 초기화 할 땐 배열크기를 명시하면 error


      //선언 후 초기화
      int[] arr5;
      arr5 = new int[]{1,2,3,4,5};
      //arr5 = {1,2,3,4,5}; //선언 이후 초기화시 new int[] 생략 불가

      arr5[0] = 1; //각 요소마다 초기화
      arr5[1] = 2;
      arr5[2] = 3;
      arr5[3] = 4;
      arr5[4] = 5;

      for(int i=0 ; i<5 ; i++){ //for문으로 초기화
         arr5[i]=i+1;
      }

   ```
1. # 출력
   ```java
      System.out.println(arr); //I@b4c966a : 시작 주소 출력
      System.out.println(Arrays.toString(arr)); //[1, 2, 3, 4, 5] : Arrays함수 이용
      System.out.println(arr[0]) //인덱스로 출력
   ```
1. # 디폴트 값
   ```java
      int[] arr = new int[5];   //int 배열
      System.out.println(Arrays.toString(arr)); //[0, 0, 0, 0, 0] : int형 초기값 0
      String[] strArray = new String[3];   //String 배열
      System.out.println(Arrays.toString(strArray)); //[null, null, null] : String형 초기값 null
   ```
1. # List
   미리 크기를 알아야 하고 한번 크기가 정해지면 고정된 크기로 계속 사용해야 하는 배열의 단점을 보안할 수 있는 프레임워크입니다.   
   1) 여러개의 데이터를 한꺼번에 다를 수 있습니다.   
   2) 메모리상에 연속되지 않아도 됩니다.   
   3) 미리 공간을 확보해 놓지 않아도 됩니다.   
   4) 필요에 따라 데이터가 늘어나거나 줄어듭니다.   
   5) 첫 번째 위치로부터 index로 목표위치를 알려면 한 칸씩 이동하면서 찾아야 합니다.   

