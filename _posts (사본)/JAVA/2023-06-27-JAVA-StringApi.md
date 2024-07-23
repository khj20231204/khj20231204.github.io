---
layout: single
title: String클래스
categories: JAVA
tag: [문자열 리터럴,String클래스,charAt,replace,subString,concat,contains,equals,indexOf,lastIndexOf,split]
---

1. # String클래스
   java.lang 패키지 내에 있는 String클래스는 문자열을 다루는데 필요한 여러가지 기능을 가지고 있습니다. 문자열을 변환, 교환, 추출, 비교, 탐색, 추가, 제거 등의 작업을 할 수 있는 메소드들을 제공합니다.

1. # 문자열 생성 방법 2가지
   2. ## 문자열 리터럴을 지정   
   &#34; &#34;로 묶어 문자열 리터럴로 만듭니다.   
   ```java
      String str = "Hello";
   ```   
   "Hello"란 문자열은 상수 풀이란 메모리 공간에 생기게 되고 그 주소를 str이 가리키게 됩니다.   

   2. ## String클래스 사용   
   주어진 문자열을 String인스턴스로 생성합니다.   
   ```java   
      String s1 = new String("hello");
      System.out.println(s1); //hello   
      String s2 = new String(new char[] {'h','e','l','l','o'});
      System.out.println(s2); //hello
   ```   
   new연산자로 생성시 힙 메모리 공간을 차지하게 됩니다.   

   2. ## 문자열과 String클래스   
   ```java
      String s1 = new String("hello");  //--㉠ 
      String s2 = new String("hello");  //--㉠ 
      System.out.println(s1 == s2);  //false
      System.out.println("s1 hashCode : "+System.identityHashCode(s1)); //s1 hashCode : 1325547227
      System.out.println("s2 hashCode : "+System.identityHashCode(s2)); //s2 hashCode : 980546781

      String str1 = "hello";  //--㉡
      String str2 = "hello";  //--㉡
      System.out.println(str1 == str2);  //true
      System.out.println("str1 hashCode : "+System.identityHashCode(str1)); //str1 hashCode : 2061475679
      System.out.println("str2 hashCode : "+System.identityHashCode(str2)); //str2 hashCode : 2061475679
   ```   
   ㉠은 서로 다른 힙 메모리 공간을 차지하기 때문에 다른 주소값을 나타냅니다.   
   ㉡는 상수 풀에 |h|e|l|l|o|란 문자열이 만들어지고 str1과 str2가 전부 이 주소를 가리키게 됩니다.   

   2. ## 문제점   
   이런 경우 힙 공간이든 상수 풀 공간이든 한번 생성된 String은 불변의 값을 가지게 됩니다. String로 선언해서 문자열을 생성한 경우 메모리 낭비가 발생할 수도 있게 됩니다. 따라서 String클래스를 사용하기 보단 StringBuilder나 StringBuffer를 사용하면 메모리 낭비를 줄일 수 있습니다.   

1. # 변환

   2. ## 바이트 배열을 문자열로 변환   
      네트워크에서 주로 주고 받는 파일 단위가 바이트기 때문에 바이트를 문자열로 변환합니다.   

      바이트를 문자열로 변환
      ```java
         byte[] byteData = {98,121,116,101,68,97,116,97}  //아스키코드 byteData

         String str1 = new String(byteData);  //byteData

         String str2 = new String(byteData, StandardCharsets.UTF_8);  //byteData

         String str3 = new String(byteData, StandardCharsets.UTF_16);  //批瑥䑡瑡

         String str4 = new String(byteData,0,4);  //byte
      ```   

      문자열과 바이트로 서로 변환    
      ```java
         String str = "byteData";

         byte[] strByte = str.getBytes();  //98,121,116,101,68,97,116,97 byteData를 바이트로 변환
         
         String strVal = new String(strByte);  //byte를 문자열로 변환
      ```

   2. ## String valueOf(char/int/long/float/double/Object)   
      * 기본타입과 object를 문자열로 반환해줍니다.   
      ```java   
         String strChar = String.valueOf('d');   
         String strInt = String.valueOf(34);   
         String strLong = String.valueOf(-323452L);   
         String strDouble = String.valueOf(0.3234);   
         Date day = new Date();   
         String strDate = String.valueOf(day);//
         
         System.out.println(strChar); //d   
         System.out.println(strInt); //34   
         System.out.println(strLong); //-323452   
         System.out.println(strDouble); //0.3234   
         System.out.println(strDate); //Tue Jun 27 14:26:17 KST 2023   
      ```   

   2. ## String toLowerCase()   
      * 모든 문자열을 소문자로 반환합니다.
      ```java
         String str = "Hello";
         System.out.println(str.toLowerCase()); //hello
      ```

   2. ## String toUpperCase()   
      * 모든 문자열을 대문자로 반환합니다.
      ```java
         String str = "Hello";
         System.out.println(str.toUpperCase()); //HELLO
      ```

1. # 교환
   2. ## String replcae(char old, char new), String replace(String old, String new)   
      * old문자나 문자열을 찾아서 new문자나 문자열로 바꾼 값을 반환합니다.
      ```java
         String str = "Hellohello";
         System.out.println(str.replace('l', 'k')); //Hekkohekko
         System.out.println(str.replace("hel", "pp")); //Hellopplo
         System.out.println(str.replace("ll", "ww")); //Hewwohewwo
      ```   

1. # 검색
   2. ## charAt(int index)      
      * index에 있는 문자를 알려줍니다.   
      ```java   
         String s1 = new String("hello");
         char c1 = s1.charAt(1);
         System.out.println(c1); //e
      ```

   2. ## contains(CharSequence s)
      * 문자열s 가 있는지 검색. 있으면 true를 반환하고, 없으면 false를 반환합니다. <span style="color:red">대소문자 구분</span>합니다.
      ```java
         String str1 = "HelloWorld";
         boolean result = str1.contains("loW");
         System.out.println(result); //true
      ```

   2. ## int indexOf(char c), int indexOf(char c, int start), int indexOf(String str)   
      * 문자나 문자열을 검색하여 찾으면 최초 발견한 index값을, 없으면 -1을 반환합니다.   
      ```java
         String str = "HelloWorld";
         System.out.println(str.indexOf('o')); //4 index 4에서
         System.out.println(str.indexOf('o',1)); //4
         System.out.println(str.indexOf('o',7)); //-1
         System.out.println(str.indexOf("owo")); //-1 대소문자 구분
         System.out.println(str.indexOf("oWo")); //4
      ```
      
   2. ## int lastIndexOf(char c), int lastIndexOf(char c, int start), int lastIndexOf(String str)
      * 문자나 문자열을 끝에서부터 오른쪽으로 검색하여 찾으면 최초 발견한 index값을, 없으면 -1을 반환합니다.   
      ```java
         String str = "HelloWorld";
         System.out.println(str.lastIndexOf('o')); //6 ← 방향으로 검색하여 최초 'o'발견 index
         System.out.println(str.lastIndexOf('o',1)); //-1 index=1부터 ← 방향으로 검색. 
         System.out.println(str.lastIndexOf('o',7)); //6 index=7부터 ← 방향으로 검색.
         System.out.println(str.lastIndexOf("or")); //6 "or"에서 'o'가 끝난 지점의 index
         System.out.println(str.lastIndexOf("Wor")); //4 "Wor"에서 'W'가 끝난 지점의 index
      ```

1. # 추출   
   2. ## String subString(int start), String subString(int start, int end)
      * start인덱스부터 문자열 끝까지 또는 start인덱스에서 end인덱스까지  해당 인덱스 범위의 문자열을 가지고 옵니다. 단 end인덱스 문자는 미포함
      ```java
         String str = "Hello";
         System.out.println(str.substring(1)); //ello
         System.out.println(str.substring(1, 4)); //ell 마지막 index4 문자 미포함
      ```

   2. ## String[] split(String sp)   
      * 문자열을 sp분리자로 분리 후 String배열에 담습니다.   
      ```java   
         String str = "gonna, wanna, havto";
         String[] strSplits = str.split(", ");
         for(String s : strSplits){
            System.out.println(s);
            }
         
         결과
         gonna
         wanna
         havto
      ```

1. # 비교
   2. ## boolean equals(Object obj)
      3. equals와 "==" 연산자
      String클래스가 Object의 equals메소드를 재정의 했기 때문에 번지(주소 값) 비교가 아닌 문자열 비교를 합니다.   
      하지만 "==" 연산자는 그래로 번지(주소 값)을 비교합니다.   
      ```java
         String str1 = new String("abc");
         String str2 = new String("abc");
         String str3 = "abc";
         
         System.out.println(str1.equals(str2)); //true. str1과 str2의 값을 비교  
         System.out.println(str1 == str2); //false. str1과 str2 각 변수에 저장된 주소 값을 비교

         System.out.println(str1.equals(str3)); //true. "abc"라는 값을 비교
         System.out.println(str1 == str3); //false. str1과 strl3 각 변수에 저장된 주소 값을 비교
      ```
      str_1과 str_2의 문자열값이 "abc"로 같기 때문에 equals메소드는 true를 리턴합니다. 하지만 연산자 "=="는 재정의(override) 하지 않았기 때문에 주소값을 비교하고 false를 리턴합니다.
      
      3. 문자열 직접 비교   
      obj가 String이 아니거나 문자열이 다르면 false를 반환합니다.   
      ```java
         String str1 = "Hello";
         char[] c = {'H','e','l','l','o'};
         System.out.println(str1.equals(c)); //false
         System.out.println(str1.equals("hello")); //false
         System.out.println(str1.equals("Hello")); //true
      ```

      __문자열 리터럴__   
      + 자바에서 문자 리터럴(데이터)은 클래스 파일 안에 리터럴 목록이 따로 존재합니다. 이 목록이 클래스 로더에 의해 메모리에 올라갈 때 JVM에 의해 Runtim Data Area(JVM 메모리영역)내부의 메소드 영역인 constant pool에 저장이 됩니다.   
      + constant pool에는 "abc"란 문자열이 하나가 있고 이 주소값이 "abc"를 저장하는 모든 객체변수에 저장이 됩니다.   
      ```java
         String str1 = "abc";
         String str2 = "abc";
         System.out.println(str1.equals(str2)); //true
         System.out.println(str1 == str2); //true
      ```   
      str1과 str2이는 constant pool에 있는 1개의 "abc" 같은 주소값을 할당 받습니다.   

1. # 추가
   2. ## concat(String str)   
   * 문자열 str을 뒤에 덧붙입니다.
   ```java
      String str1 = "Hello";
      str1 = str1.concat("World");
      System.out.println(str1); //HelloWorld
   ```

1. # 제거
   2. ## String trim()
      * 양쪽 끝 공백을 제거합니다. 단, <span style="color:red">문자열 중간 공백은 제거되지 않습니다.</span>
      ```java
         String str = " Hello World ";
         System.out.println(str.trim()); //Hello World
      ```
   


