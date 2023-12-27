---
layout: single
title: StringBuffer클래스
categories: JAVA
tag: [StringBuffer,equals,toString,charAt,replace,subString]
---

java의 정석 교재에 있는 예제입니다.

1. ## StringBuffer을 사용하는 이유
   String클래스는 문자열을 변경하면 새로운 메모리 주소를 할당 받아서 입력하지만 StringBuffer클래스는 동일한 메모리 주소에 값을 변경합니다. 그래서 리소스를 절약하기 위해서 문자열을 다루는 작업이 있으면 string대신 StringBuffer나 StringBuilder를 사용합니다.
   StringBuffer sb1과 Sring str1에 각각 문자열을 넣고 그 값을 sb2, str2에 입력 후 sb1과 str1에 문자열을 추가했을 때 sb2와 str2의 값을 보겠습니다.
   ```java
      StringBuffer sb1 = new StringBuffer("abc"); //sb1="abc" 입력
      StringBuffer sb2 = sb1; //sb1을 sb2에 할당
      sb1.append(" def"); //sb1에 def 추가
      System.out.println("sb1:"+ sb1 + " ,sb2:"+sb2); //sb1:abc def ,sb2:abc def

      String str1 = new String("abc"); //str1="abc" 입력
      String str2 = str1; //str1을 str2에 할당
      str1  += " def"; //str1에 def 추가
      System.out.println("str1:"+ str1 + " ,str2:"+str2); //str1:abc def ,str2:abc
   ```
   sb1과 sb2는 같은 문자열 "abc"의 주소를 할당 받았기 때문에 "abc" 문자열에 " def"를 추가했을 때 같은 값이 출력됩니다.   
   하지만 String변수인 str1은 str1 += "def"를 했을 때 메모리에 새로운 문자열 주소를 할당 받고 그 주소에 "abc def"란 문자열을 입력하게 됩니다. 그리고  str2는 str1의 기존의 주소를 그대로 참조하고 있기 때문에 서로 값이 다르게 나오게 됩니다.
1. ## equals()메소드와 toString()메소드
   String클래스는 equals를 오버라이딩해서 == 와 다른 결과를 가지고 옵니다. equals는 문자열 값 비교, ==(등가비교연사자)는 객체가 참조하고 있는 주소를 비교.  
   StringBuffer클래스의 equals는 오버라이딩하지 않았기 때문에 ==와 같은 결과를 가지고 옵니다.
   toString()메소드는 String클래스와 StringBuffer클래스 모두 오버라이딩했기 때문에 문자열을 가지고 옵니다.
   ```java
      String str1 = new String("abc"); 
      String str2 = new String("abc");
      System.out.println(str1.equals(str2)); //true
      System.out.println(str1 == str2); //false
      System.out.println(str1.toString()); //abc

      StringBuffer sb1 = new StringBuffer("abc"); 
      StringBuffer sb2 = new StringBuffer("abc");
      System.out.println(sb1.equals(sb2)); //false
      System.out.println(sb1 == sb2); //false
      System.out.println(sb1.toString()); //abc
   ```
1. ## 기본 버퍼의 크기
   SringBuffer의 기본 char[idx]의 크기는 idx=16으로 16개의 문자를 저장할 수 있습니다. 16개의 문자 길이를 넘으면 내부적으로 버퍼의 크기를 증가시키고 이전 배열의 값을 복사합니다.
1. ## StringBuffer클래스의 메소드들
   1. ### charAt(int index)
      index 위치에 있는 문자를 반환합니다.
      ```java
         StringBuffer sb1 = new StringBuffer("hello kitty");
         char c = sb1.charAt(1);
         System.out.println(c); //e
      ```
   1. ### StringBuffer replce(int start, int end, String str), StringBuffer replce(int start, String str)
   start부터 end까지 범위를 str문자열로 바꾼다. 단 end는 포함되지 않습니다.
   ```java
      StringBuffer sb1 = new StringBuffer("hello");
      sb1.replace(2, 3,"aaa");
      System.out.println(sb1); //heaaalo
   ```
   1. ### String subString(int start), String subString(int start, int end)
   start부터 문자열 끝까지 또는 start부터 end까지 해당 인덱스 범위의 문자열을 가지고 옵니다. 단 끝 인덱스 문자는 미포함.
   ```java
      StringBuffer sb1 = new StringBuffer("hello kitty");
      String str = sb1.substring(6);
      System.out.println(str); //kitty
      str = sb1.substring(0,5); //hello
      System.out.println(str);
   ```
   1. ### StringBuffer append(boolean/char/char[]/double/float/int/long/Object/String)
   매개변수들을 문자열로 변환하여 문자열 뒤에 붙입니다.
   ```java
      StringBuffer sb = new StringBuffer("abc");
      char[] arr = {'e','f','g'};
      sb.append(" ,"+true).append(" ,"+'d'+" ,").append(arr).append(" ,"+0.3454d).append(" ,"+34).append(" ,END");
      System.out.println(sb);
   ```
   1. ### int capacity(), int length()
   capacity()는 버퍼의 크기를 반환하고 length()는 문자열의 길이를 반환합니다.
   ```java
      StringBuffer sb1 = new StringBuffer();
      StringBuffer sb2 = new StringBuffer("a");
      System.out.println("sb1.capacity():"+sb1.capacity()+" ,sb1.length():"+sb1.length()); //sb1.capacity():16 ,sb1.length():0
      System.out.println("sb1.capacity():"+sb2.capacity()+" ,sb1.length():"+sb2.length()); //sb1.capacity():17 ,sb1.length():1
   ```
   1. ### StringBuffer delete(int start, int end)
   start부터 end까지 문자를 제거합니다. 단 end위치의 문자는 제외됩니다.
   ```java
      StringBuffer sb1 = new StringBuffer("hello kitty");
      StringBuffer sb2 = sb1.delete(1,6); 
      System.out.println(sb2); //hkitty 공백자리가5, 'k'자리가 6
   ```
   1. ### StringBuffer deleteCharAt(int index)
   index 위치의 문자를 삭제합니다.
   ```java
      StringBuffer sb1 = new StringBuffer("hello kitty");
      StringBuffer sb2 = sb1.deleteCharAt(5); //5위치는 공백
      System.out.println(sb2); //hellokitty
   ```
   1. ### StringBuffer insert(int idx, boolean/char/char[]/double/float/int/long/Object/String)
   두 번째 매개변수로 받은 값을 문자열로 변환 후 idx 위치에 추가합니다.  
   ```java
      StringBuffer sb1 = new StringBuffer("hello");
      sb1.insert(2," , " +'a'+ " , ");
      char[] arr = {'b','c','d'};
      sb1.insert(2,  arr);
      sb1.insert(2, " , " + 101+ " , ");
      sb1.insert(2, " , new");
      System.out.println(sb1); //he , new , 101 , bcd , a , llo
   ```
   1. ### StringBuffer reverse()
   문자열의 순서를 거꾸로 나열합니다.
   ```java
      StringBuffer sb1 = new StringBuffer("hello kitty");
      System.out.println(sb1.reverse()); //yttik olleh   
   ```
   1. ### void setCharAt(int idx, char ch)
   idx위치의 문자를 ch로 바꿉니다.
   ```java
      StringBuffer sb1 = new StringBuffer("hello");
      sb1.setCharAt(1,'a');
      System.out.println(sb1); //hallo
   ```
   1. ### String toString()
   StringBuffer를 toString로 반환
   ```java
      StringBuffer sb1 = new StringBuffer("hello");
      String str = sb1.toString();
      //System.out.println(str instanceof StringBuffer); error 발생
      System.out.println(str instanceof String); //true
   ```
1. ## StringBuffer와 StringBuilder
StringBuffer에서 쓰레드의 동기화 기능만 뺀 것이 StringBuilder입니다. 그외 기능은 완전 동일하기 때문에 위에 예제들에서 StringBuffer를 StringBuilder로만 바꿔서 사용하시면 됩니다. 멀티 쓰레드에서 동기화 기능을 사용하기 위해선 StringBuffer를, 싱글 쓰레드에서 사용하기 위해선 StringBuilder를 사용하시면 됩니다.



   

   