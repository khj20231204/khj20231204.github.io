---
layout: single
title: String클래스
categories: JAVA
tag: [문자열 리터럴,String클래스,charAt,replace,subString,concat,contains,equals,indexOf,lastIndexOf,split]
---

1. ## String클래스
   java.lang 패키지 내에 있는 String클래스는 문자열을 다루는데 필요한 여러가지 기능을 가지고 있습니다. 문자열을 추출, 비교, 변환, 탐색, 분리 등의 작업을 할 수 있는 메소드들을 제공합니다.

1. ## 문자열 생성 방법 2가지
   - ### 문자열 리터럴을 지정   
   &#34; &#34;로 묶어 문자열 리터럴로 만듭니다.   
   ```java
      String str = "Hello";
   ```   

   - ### String클래스 사용   
   주어진 문자열을 String인스턴스로 생성합니다.   
   ```java   
      String s1 = new String("hello");
      System.out.println(s1); //hello   
      String s2 = new String(new char[] {'h','e','l','l','o'});
      System.out.println(s2); //hello
   ```   

1. ## 바이트 배열을 문자열로 변환
   네트워크에서 주로 주고 받는 파일 단위가 바이트기 때문에 바이트를 문자열로 변환합니다.   

   다양한 방법으로 문자열 객체를 생성할 수 있습니다.   
   ```java
      String()
      String(byte[] bytes)
      String(byte[] bytes, Charset charset)
      String(byte[] ascii, int hibyte)
      String(byte[] bytes, int offset, int length)
      String(byte[] bytes, int offset, int length, Charset charset)
      String(byte[] ascii, int hibyte, int offset, int count)
      String(byte[] bytes, int offset, int length, String charsetName)
      String(byte[] bytes, String charsetName)
      String(char[] value)
      String(char[] value, int offset, int count)
      String(int[] codePoints, int offset, int count)
      String(String original)
      String(StringBuffer buffer)
      String(StringBuilder builder)
   ```   
   
   바이트를 받는 예제   
   ```java
      byte[] byteData = {98,121,116,101,68,97,116,97}  //아스키코드

   ```

1. ## charAt(int index)      
   * index에 있는 문자를 알려줍니다.   
   ```java   
      String s1 = new String("hello");
      char c1 = s1.charAt(1);
      System.out.println(c1); //e
   ```
1. ## String replcae(char old, char new), String replace(String old, String new)
   * old문자나 문자열을 찾아서 new문자나 문자열로 바꾼 값을 반환합니다.
   ```java
      String str = "Hellohello";
      System.out.println(str.replace('l', 'k')); //Hekkohekko
      System.out.println(str.replace("hel", "pp")); //Hellopplo
      System.out.println(str.replace("ll", "ww")); //Hewwohewwo
   ``` 
1. ## String subString(int start), String subString(int start, int end)
   * start인덱스부터 문자열 끝까지 또는 start인덱스에서 end인덱스까지  해당 인덱스 범위의 문자열을 가지고 옵니다. 단 end인덱스 문자는 미포함
   ```java
      String str = "Hello";
      System.out.println(str.substring(1)); //ello
      System.out.println(str.substring(1, 4)); //ell 마지막 index4 문자 미포함
   ```
1. ## concat(String str)   
   * 문자열 str을 뒤에 덧붙입니다.
   ```java
      String str1 = "Hello";
      str1 = str1.concat("World");
      System.out.println(str1); //HelloWorld
   ```
1. ## contains(CharSequence s)
   * 문자열s 가 있는지 검색. 있으면 true를 반환하고, 없으면 false를 반환합니다. <span style="color:red">대소문자 구분</span>합니다.
   ```java
      String str1 = "HelloWorld";
      boolean result = str1.contains("loW");
      System.out.println(result); //true
   ```
1. ## boolean equals(Object obj)

   2. equals와 "==" 연산자
   String클래스가 Object의 equals메서드를 재정의 했기 때문에 번지(주소 값) 비교가 아닌 문자열 비교를 합니다.   
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
   str_1과 str_2의 문자열값이 "abc"로 같기 때문에 equals메서드는 true를 리턴합니다. 하지만 연산자 "=="는 재정의(override) 하지 않았기 때문에 주소값을 비교하고 false를 리턴합니다.
   
   2. 문자열 직접 비교   
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

1. ## int indexOf(char c), int indexOf(char c, int start), int indexOf(String str)   
   * 문자나 문자열을 검색하여 찾으면 최초 발견한 index값을, 없으면 -1을 반환합니다.   
   ```java
      String str = "HelloWorld";
      System.out.println(str.indexOf('o')); //4 index 4에서
      System.out.println(str.indexOf('o',1)); //4
      System.out.println(str.indexOf('o',7)); //-1
      System.out.println(str.indexOf("owo")); //-1 대소문자 구분
      System.out.println(str.indexOf("oWo")); //4
   ```
1. ## int lastIndexOf(char c), int lastIndexOf(char c, int start), int lastIndexOf(String str)
   * 문자나 문자열을 끝에서부터 오른쪽으로 검색하여 찾으면 최초 발견한 index값을, 없으면 -1을 반환합니다.   
   ```java
      String str = "HelloWorld";
      System.out.println(str.lastIndexOf('o')); //6 ← 방향으로 검색하여 최초 'o'발견 index
      System.out.println(str.lastIndexOf('o',1)); //-1 index=1부터 ← 방향으로 검색. 
      System.out.println(str.lastIndexOf('o',7)); //6 index=7부터 ← 방향으로 검색.
      System.out.println(str.lastIndexOf("or")); //6 "or"에서 'o'가 끝난 지점의 index
      System.out.println(str.lastIndexOf("Wor")); //4 "Wor"에서 'W'가 끝난 지점의 index
   ```
1. ## String[] split(String sp)   
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
1. ## String toLowerCase()
   * 모든 문자열을 소문자로 반환합니다.
   ```java
      String str = "Hello";
      System.out.println(str.toLowerCase()); //hello
   ```
1. ## String toUppercase()
   * 모든 문자열을 대문자로 반환합니다.
   ```java
      String str = "Hello";
      System.out.println(str.toUpperCase()); //HELLO
   ```
1. ## String trim()
   * 양쪽 끝 공백을 제거합니다. 단, <span style="color:red">문자열 중간 공백은 제거되지 않습니다.</span>
   ```java
      String str = " Hello World ";
      System.out.println(str.trim()); //Hello World
   ```
1. ## String valueOf(char/int/long/float/double/Object)
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
  


