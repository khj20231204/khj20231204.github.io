---
layout: single
title: char형 변환
categories: JAVA
tag: [char형변환]
---
```java
   /*
   char은 10이상의 숫자는 입력 안된다. 아스키코드에 있는 문자숫자가
   9까지 밖에 없다.

   1.int, long, double -> char
   *int i_1 = 44; long l_1 = 100; double d_1 = 3.14;
   *숫자로 9이상의 값을 char넣을 순 있지만 정확한 값을 가져올 순 없다
   	아스키코드에 있는 문자숫자가 9까지밖에 없기 때문이다.

   2.char -> int, long, double

   3.int[], long[], double[] -> char[]
   4.char[] -> int[], long[], double[]

   5.char -> byte
   6.byte -> char

   7.char[] -> byte[]
   8.byte[] -> char[]

   9.char[] -> String
   10.String -> char[]

   String이 1글자 일 때
   11.char -> String
   12.String -> char
   */

   //1.int, long, double -> char : 더하기'0' 이후 강제타입변환
   //1)더하기'0' 이후 강제타입변환
   int i_1 = 4; long l_1 = 9; double d_1 = 3;
   char c_i_1 = (char)(i_1+'0');
   char c_l_1 = (char)(l_1+'0');
   char c_d_1 = (char)(d_1+'0');
   System.out.println("1-1)c_i_1:"+c_i_1+" ,c_l_1:"+c_l_1+" ,c_d_1:"+c_d_1); //1-1)c_i_1:4 ,c_l_1:9 ,c_d_1:3
   //2)int를 char로 변환은 Character.forDigit()도 이용 가능
   char c_1 = Character.forDigit(i_1, 10);//10은 10진수를 의미
   System.out.println("1-2)forDigit:"+c_1); //1-2)forDigit:4

   //2.char -> int, long, double : 빼기'0', Character.getNumbericValue이용
   //1)아스키코드 활용
   char c_2 = '7';
   int i_2 = c_2 - '0';
   long l_2 = c_2 - '0';
   double d_2 = c_2 - '0';
   System.out.println("2-1)i_2:"+i_2+" ,l_2:"+l_2+" ,d_2:"+d_2); //2-1)i_2:7 ,l_2:7 ,d_2:7.0
   //2)char을 int로 변환은 getNumbericValue()도 이용 가능
   i_2 = Character.getNumericValue(c_2);
   System.out.println("2-2)getNumericValue:"+i_2); //2-2)getNumericValue:7

   //3.int[], long[], double[] -> char[]
   //for문으로
   //4.char[] -> int[], long[], double[]
   //for문으로

   //5.char -> byte : 강제타입변환
   char c_5 = 'c';
   byte b_5 = (byte)c_5;
   System.out.println("char->byte:"+b_5); //char->byte:99

   //6.byte -> char : 강제타입변환
   b_5 = 0x09; //아스키코드 10진수:9, 문자:HT
   c_5 = (char)0x52;
   System.out.println("byte->char:"+c_5); //byte->char:R

   int count=0;

   //7.char[] -> byte[] : for문으로 각각
   char[] charArray_7 = {'a','b','c','d'};
   byte[] byteArray_7 = new byte[charArray_7.length];
   count = 0;
   for(char i : charArray_7) {
      byteArray_7[count] = (byte)i;
      System.out.println(byteArray_7[count]); //97 98 99 100
      count++;
   }

   //8.byte[] -> char[] : for문으로 각각
   byte[] byteArray_8 = { 0x64, 0x65, 0x66, 0x67 }; //10진수로 100,101,102,103
   char[] charArray_8 = new char[byteArray_8.length];
   count = 0;
   for(byte b : byteArray_8) {
      charArray_8[count] = (char)b;
      System.out.println(charArray_8[count]); //d e f g
      count++;
   }

   //9.char[] -> String : String.valueOf, String클래스 생성자 이용
   //1)String.valueOf()이용
   char[] charArray_9 = {'a','b','c','d'};
   String str_9 = String.valueOf(charArray_9);
   System.out.println("9-1)"+str_9); //9-1)abcd
   //2)String클래스 생성자 이용
   str_9 = new String(charArray_9);
   System.out.println("9-2)"+str_9); //9-2)abcd

   //10.String -> char[] : toCharArray()이용
   String str_10 = "difficult hard";
   char[] charArray_10 = str_10.toCharArray();
   for(char c : charArray_10) {
      System.out.print(c); //difficult hard
   }
   System.out.println();

   //String이 1글자 일 때
   //11.char -> String (Character.toString이용, String.valueOf이용)
   //1)Character.toString이용
   char c_11 = 'c';
   String str_11 = Character.toString(c_11);
   System.out.println("11-1)"+str_11); //11-1)c
   //2)String.valueOf이용
   str_11 = String.valueOf(c_11);
   System.out.println("11-2)"+str_11); //11-2)c

   //12.String -> char (charAt이용)
   String str_12 = "s";
   char c_12 = str_12.charAt(0);
   System.out.println("12)"+c_12); //12)s

```