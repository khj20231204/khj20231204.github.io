---
layout: single
title: String형 변환
categories: JAVA
tag: [String형변환]
---
```java 
   /*
	1.int, long, double -> String
	2.String -> int, long, double

	3.int[], long[], double[] -> String
	4.String -> int[], long[], double[]

	5.String -> byte
	6.byte -> String

     7.byte[] -> String
	8.String -> byte[]

	9.char[] -> String
	10.String -> char[]

	String이 1글자 일 때
	11.char -> String
	12.String -> char
	*/

     //1.int, long, double -> String : String.valueOf(), Integer.toString()이용
     //1)String.valueOf()이용
     int i_1 = 100; long l_1 = 1000; double d_1 = 34.45;
     String str_1_int = String.valueOf(i_1);
     String str_1_long = String.valueOf(l_1);
     String str_1_double = String.valueOf(d_1);
     System.out.println("1-1) int:"+str_1_int+" ,long:"+str_1_long+" ,double:"+str_1_double); //1-1) int:100 ,long:1000 ,double:34.45
     //2)Integer/Long/Double.toString이용
     str_1_int = Integer.toString(i_1);
     str_1_long = Long.toString(l_1);
     str_1_double = Double.toString(d_1);
     System.out.println("1-2) int:"+str_1_int+" ,long:"+str_1_long+" ,double:"+str_1_double); //1-2) int:100 ,long:1000 ,double:34.45

     //2.String -> int, long, double : 타입.parse.. 이용
     String str_2 = "3424";
     int i_2 = Integer.parseInt(str_2);
     long l_2 = Long.parseLong(str_2);
     double d_2 = Double.parseDouble(str_2);
     System.out.println("2) int:"+i_2+" ,long:"+l_2+ " ,double:"+d_2); //2) int:3424 ,long:3424 ,double:3424.0

     //3.int[], long[], double[] -> String : Arrays.toString()이용
     int[] i_3 = {34, 454}; long[] l_3 = {1432, 324324}; double[] d_3 = {34.45, 54.34};
     String str_3_int = Arrays.toString(i_3);
     String str_3_long = Arrays.toString(l_3);
     String str_3_double = Arrays.toString(d_3);
     System.out.println("3-1) int:"+str_3_int+" ,long:"+str_3_long+" ,double:"+str_3_double); //3-1) int:[34, 454] ,long:[1432, 324324] ,double:[34.45, 54.34]

     //4.String -> int[], long[], double[] : charAt-'0', Stream이용
     //1)charAt-'0' 이용
     String str_4 = "453462";
     int[] digits = new int[str_4.length()];
     for(int i=0 ; i<str_4.length() ; i++){
         digits[i] = str_4.charAt(i)-'0';  //빼기 '0'
     }
     System.out.println(Arrays.toString(digits)); //[4, 5, 3, 4, 6, 2]
     //2)Stream - 람다를 알아야한다. 나중에

     //5.String -> byte
     //없다
     //6.byte -> String
     //없다

     //7.byte[] -> String : new String클래스 생성자, toString이용
     //1)String클래스 생성자 이용
     byte[] byteArray_7 = { 0x64, 0x65, 0x66, 0x67 }; //10진수:100,101,102,103, 문자:d,e,f,g
     //String str_7 = new String(byteArray_7); 또는 밑에처럼 UTF_8설정
     String str_7 = new String(byteArray_7, StandardCharsets.UTF_8);
     System.out.println("String클래스 이용:"+str_7); //String클래스 이용:defg
     //2)Arrays.toString이용 - 10진수 출력
     str_7 = Arrays.toString(byteArray_7);
     System.out.println("toString():"+str_7); //toString():[100, 101, 102, 103]

     //8.String -> byte[] : getBytes()이용
     String str_8 = "difficult hard";
     //byteArray_8 = str_8.getBytes(); 또는 밑에처럼 UTF_8 설정
     byte[] byteArray_8 = str_8.getBytes(StandardCharsets.UTF_8);
     for(byte b : byteArray_8){
         System.out.print((char)b); //difficult hard
     }

     //9.char[] -> String : String.valueOf이용, String클래스 생성자 이용
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
     //11.char -> String : Character.toString이용, String.valueOf이용
     //1)Character.toString이용
     char c_11 = 'c';
     String str_11 = Character.toString(c_11);
     System.out.println("11-1)"+str_11); //11-1)c
     //2)String.valueOf이용
     str_11 = String.valueOf(c_11);
     System.out.println("11-2)"+str_11); //11-2)c

     //12.String -> char : charAt이용
     String str_12 = "s";
     char c_12 = str_12.charAt(0);
     System.out.println("12)"+c_12); //12)s
```