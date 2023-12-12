---
layout: single
title: Byte형 변환
categories: JAVA
tag: [Byte형변환]
---
```java 
   /*
	byte에 HEX(16진수)를 넣었을 때
	int, short, long, double이면 10진수를
	char이면 문자를 출력

	1.int, long, double -> byte
	2.byte -> int, long, double

	3.int[], long[], double[] -> byte[]
	4.byte[] -> int[], long[], double[]

	5.char -> byte
	6.byte -> char

	7.char[] -> byte[]
	8.byte[] -> char[]

	9.byte[] -> String
	10.String -> byte[]
	*/

     //1.int, long, double -> byte : 강제타입변환
     int i_1 = 10; long l_1 = 100; double d_1 = 3.14;
     byte b_1 = (byte)i_1;
     System.out.println("int:"+b_1); //int:10
     b_1 = (byte)l_1;
     System.out.println("long:"+b_1); //long:100
     b_1 = (byte)d_1;
     System.out.println("double:"+b_1); //double:3

     //2.byte -> int, long, double : 강제타입변환
     byte b_2 = 0x11; //유니코드50은 숫자2
     System.out.println((int)b_2); //17
     System.out.println((long)b_2);  //17
     System.out.println((double)b_2);  //17.0

     //3.int[], long[], double[] -> byte[] : for문으로 하나씩 변환
     int[] iArray_3 = new int[] {3,5,8,2};
     byte[] byteArray_3 = new byte[iArray_3.length];
     int count=0;
     for(int i : iArray_3) {
         byteArray_3[count] = (byte)i;
         System.out.println(byteArray_3[count]); //3 5 8 2
         count++;
     }

     //4.byte[] -> int[], long[], double[] - 바꿀 필요 없다, 찾아도 없다
     byte[] byteArray_4 = { 0x00, 0x01, 0x03, 0x09 }; //10진수로 0,1,3,9
     System.out.println(ByteBuffer.wrap(byteArray_4).getInt()+ " "); //66313
     //System.out.println(ByteBuffer.wrap(byteArray_4).getDouble()+ " "); error발생
     //System.out.println(ByteBuffer.wrap(byteArray_4).getLong()+ " "); error발생

     //5.char -> byte : 강제타입변환
     char c_5 = 'c';
     byte b_5 = (byte)c_5;
     System.out.println("char->byte:"+b_5); //char->byte:99

     //6.byte -> char : 강제타입변환
     b_5 = 0x09; //아스키코드 10진수:9, 문자:HT
     c_5 = (char)0x52;
     System.out.println("byte->char:"+c_5); //byte->char:R

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
     byte[] byteArray_8 = { 0x64, 0x65, 0x66, 0x67 }; //10진수로 0,1,3,9
     char[] charArray_8 = new char[byteArray_8.length];
     count = 0;
     for(byte b : byteArray_8) {
         charArray_8[count] = (char)b;
         System.out.println(charArray_8[count]); //d e f g
         count++;
     }

     //9.byte[] -> String : new String클래스 생성자, toString이용
     //1)String클래스 생성자 이용 - 문자 출력
     byte[] byteArray_9 = { 0x64, 0x65, 0x66, 0x67 }; //10진수:100,101,102,103, 문자:d,e,f,g
     //String str_9 = new String(byteArray_9); 또는 밑에처럼 UTF_8설정
     String str_9 = new String(byteArray_9, StandardCharsets.UTF_8);
     System.out.println("String클래스 이용 : "+str_9); //String클래스 이용 : defg
     //2)Arrays.toString이용 - 10진수 출력
     str_9 = Arrays.toString(byteArray_9);
     System.out.println("toString():"+str_9); //toString():[100, 101, 102, 103]

     //10.String -> byte[] : getBytes()이용
     String str_10 = "difficult hard";
     //byteArray_10 = str_10.getBytes(); 또는 밑에처럼 UTF_8 설정
     byte[] byteArray_10 = str_10.getBytes(StandardCharsets.UTF_8);
     for(byte b : byteArray_10){
         System.out.print((char)b); //difficult hard
     }
```