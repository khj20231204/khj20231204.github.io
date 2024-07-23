---
layout: single
title: StringTokenizer클래스
categories: JAVA
tag: [StringTokenizer,구분자]
---

1. # StringTokenizer란?
   문자열을 구분자로 나눌 때 사용합니다. 구분자는 사용자가 정할 수 있으며 기본값은 공백입니다. 구분자로 나눈 각각의 값을 토큰이라 하며 nextToken이란 메소드를 활용하여 값을 불러옵니다.
1. # 메소드
   2. <strong>int countTokens()</strong>
      전체 토큰의 수를 반환합니다.
   2. __boolean hasMoreTokens()__
      토큰이 남아있는지 알려줍니다.
   2. __String nextToken()__
      다음 토큰을 반환합니다.
1. # StringTokenizer(String str, String delim)
   str문자열을 delim구분자로 나눕니다.
    ```java
         String str = "abc def gh i jkl"; //공백으로 구분
           StringTokenizer st = new StringTokenizer(str); //구분자를 정하지 않으면 기본값 공백으로 나눕니다.
           while(st.hasMoreTokens()){
               System.out.println(st.nextToken());
           }
         결과:
         abc
         def
         gh
         i
         jkl
      ```
      ','로 구분하기
      ```java
          String str2 = "abc,def,gh,i,jkl"; //,로 구분
           st = new StringTokenizer(str2,",");
           while (st.hasMoreTokens()){
               System.out.println(st.nextToken());
           }
         결과:
         abc
         def
         gh
         i
         jkl
      ```
1. # StringTokenizer(String str, String delim, boolean t)
   마지막 인수를 true로 설정하면 구분자도 토큰으로 간주합니다.
   ```java
      String str2 = "abc,def,gh,i,jkl";
        st = new StringTokenizer(str2,",", true);
        while (st.hasMoreTokens()){
            System.out.println(st.nextToken());
        }
      결과:
      abc
      ,
      def
      ,
      gh
      ,
      i
      ,
      jkl
   ```
1. # 구분자 여러개
   StringTokenizer(String str, String delim)에서 delim값 전체를 하나의 구분자로 보는 것이 아니라 각각 문자 하나를 구분자로 본다.
   ```java
      String str3 = "xs=334+544*675";
        StringTokenizer st3 = new StringTokenizer(str3,"=+*");
        while (st3.hasMoreTokens()){
            String s = st3.nextToken();
            System.out.println("s:"+s);
        }
      결과:
      xs
      334
      544
      675
   ```
   ```java
      String str4 = "수학,34|영어,55";
        StringTokenizer st4 = new StringTokenizer(str4,",|");
        while (st4.hasMoreTokens()){
            String s = st4.nextToken();
            System.out.println("s:"+s);
        }
      결과:
      수학
      34
      영어
      55
   ```


