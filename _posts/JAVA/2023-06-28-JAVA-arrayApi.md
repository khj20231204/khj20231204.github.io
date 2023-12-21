---
layout: single
title: Arrays클래스
categories: JAVA
tag: [Arrays,배열,sort,copyOf,copyOfRange]
---

1. # 배열
   1) 여러개의 데이터를 한꺼번에 다룰 때 사용합니다.   
   2) Array는 Object는 아니지만 Referece Value로 취급됩니다.   
   3) 메모리상에 연달아 공간을 확보합니다.   
   4) 미리 공간을 확보해 놓고 써야 합니다.   
   5) 한 번 만들어진 공간은 크기가 고정됩니다.   
   6) 값은 index로 접근합니다. 
   
1. # 배열의 선언과 생성  
   ```java
      //배열 선언(배열을 다루기 위한 참조 변수 arr선언)        
      int[] arr; 
      
      //배열 생성(실제 저장 공간을 생성)
      arr = new int[5]; 

      int[] arr2 = new int[5];
   ```
   배열의 선언은 단지 참조변수를 선언한 것뿐입니다.   
   배열의 선언 - 타입[] 변수이름;   
   
   배열을 생성해야 값을 저장하기 위한 공간이 메모리에 할당됩니다.   
   배열의 생성 - 변수이름 = new 타입[크기]   
   
   보통 선언과 생성을 한꺼번에 작성합니다.   
   타입[] 변수이름 = new 타입[크기];   

1. # 배열의 초기화
   - 초기화 하는 방법   
   ```java
      //선언, 생성과 동시 초기화
      int[] arr = new int[]{1,2,3,4};
         String[] str = new String[]{"a","b","c"};

      //바로 초기화 시 new int[] 생략 가능
      int[] arr3 = {1,2,3,4,5}; 

      //null 대입 한 이후 다음에 초기화 가능
      //단, 선언 이후 초기화시 new int[] 생략 불가
         int[] arr3 = null; 
      arr3 = new int[]{1,2,3,4}; 
   ```   

   - 초기화시 error 발생하는 경우   
   ```java   
      //선언 시 초기화 할 때 배열크기를 명시하면 error
      int[] arr = new int[5]{1,2,3,4,5};  //☜error 

    //선언 시 초기화 할 땐 배열크기를 명시하면 
    String[] str = new String[3]{"a","b","c"};  //☜error

      //배열을 선언한 후 다른 실행문에서 중괄호를 사용한 배열생성은 에러가 발생됩니다.
      int[] arr = new int[5];
      arr = {1,2,3,4};  //☜error 

      int[] arr;
      arr = {1,2,3,4};  //☜error 
   ```   

   - 초기화를 하지않으면 다음과 같이 자동 초기화됩니다.   
   ```java
      byte[] arrByte = new byte[3]; //0으로 초기화
      int[] arrInt = new int[3]; //전부 0으로 초기화
      char[] arrChar = new char[3]; //'\u0000'으로 초기화
      double[] arrDouble = new double[3]; //0.0으로 초기화
      long[] arrLong = new long[3]; //0L로 초기화
      String[] arrStr = new String[3]; //null로 초기화
      boolean[] arrBoolean = new boolean[3]; //false로 초기화
   ```   

   1. # 배열의 크기
   length는 메서드가 아니라 속성값이라 lenght()이렇게 사용하지 않습니다.   
   ```java
      int[] arr = new arr[5];
      int len = arr.length; //length
   ```   
   하지만 String타입은 length()를 사용합니다.   
   ```java
      String str = "String Array";
      int len = str.length(); //length()
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

1. # 배열에 사용되는 메서드들
   ```java
      /** fill-배열 초기화 **/
      Arrays.fill(arrInt,6);
      Arrays.fill(arrStr, "korea");
      System.out.println(Arrays.toString(arrInt)); //[6, 6, 6]
      System.out.println(Arrays.toString(arrStr)); //[korea, korea, korea]

      /** toArray-리스트를 배열로 변환 **/
      LinkedList<Integer> listInt = new LinkedList<>(); //list생성
      listInt.add(1); // 데이터 삽입
      listInt.add(2);
      Integer[] arrList = new Integer[listInt.size()]; //배열 생성
      listInt.toArray(arrList); //toArray사용
      System.out.println(Arrays.toString(arrList)); //[1, 5, 3]

      List<String> listStr = new ArrayList<String>(); //list생성
      listStr.add("south");
      listStr.add("korean");
      String[] arrStr = listStr.toArray(new String[listStr.size()]); //배열 생성과 toArray대입
      System.out.println(Arrays.toString(arrStr)); //[south, korean]

      /** copyOf(원본배열, 복사할길이)-배열 전체 복사 **/
     int[] arr = {4,2,9,3,8};
     int[] arr2 = Arrays.copyOf(arr, arr.length); //arr2 = {4,2,9,3,8}
     int[] arr3 = Arrays.copyOf(arr, 3); //arr3 = {4,2,9}
     int[] arr4 = Arrays.copyOf(arr, 7); //arr4 = {4,2,9,3,8,0,0}
     /** copyOfRange(원본배열, 시작인덱스, 끝인덱스)-배열 일부 복사**/
     int[] arr5 = Arrays.copyOfRange(arr, 1,2); //arr5 = {2}, 첨자1부터 첨자(2-1)까지
     int[] arr6 = Arrays.copyOfRange(arr, 1,4); //arr5 = {2,9,3}, 첨자1부터 첨자(4-1)까지

     /** sort-정렬 **/
     Arrays.sort(arr);
     for(int i : arr){
         System.out.print(i); //23489
     }
     char[] arr_char = {'c','e','p','q','d','p'};
     Arrays.sort(arr_char);
     for(char c : arr_char){
         System.out.print(c); //cdeppq
     }

     /** binarySearch-검색:반드시 정렬이 된 상태여야 정확한 값을 얻을 수 있다 **/
     int idx = Arrays.binarySearch(arr,8);
     System.out.println("idx:"+idx); //idx:3
     idx = Arrays.binarySearch(arr_char,'p'); //2개면 제일 처음 index값
     System.out.println("idx:"+idx); //idx:4

     /** toString-문자열 리터:일차원 배열에서만 사용 가능 **/
     System.out.println(Arrays.toString(arr)); //[2, 3, 4, 8, 9]
     System.out.println(Arrays.toString(arr_char)); //[c, d, e, p, p, q]

     /** asList-배열을 리스트에 담는다 **/
     List<Integer> list = Arrays.asList(1,2,3,4);
   ```
