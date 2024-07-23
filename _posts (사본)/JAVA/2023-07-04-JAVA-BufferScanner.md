---
layout: single
title: BufferReader와 Scanner
categories: JAVA
tag: [BufferedReader, Scanner, 개행문자]
---
1. # BufferReader와 Scanner 비교
   1)처리속도   
   BufferReader는 버퍼를 사용하기 때문에 Scanner보다 속다가 빠릅니다. Scanner는 한 문자를 입력할 때마다 프로그램으로 문자가 전달되는 방식이고, BufferReader는 버퍼를 사용하기 때문에 버퍼가 다 차거나(디폴트 8192문자=16384byte) 개행문자를 만나면 프로그램으로 데이터를 전달하게 됩니다. 택배 상자를 나를 때 한 박스씩 나르는 것 보다 수레에 한번에 실어서 나르면 더 빠른 것과 비슷한 원리인 것 같습니다.   
   ```java
      String str = "";
    	
    	long start1 = System.nanoTime();
    	BufferedReader bufferTest = new BufferedReader(new FileReader("c:\\speed.txt"));
    	while((str=bufferTest.readLine()) != null) {
    		System.out.println(str);
    	}
    	long end1 = System.nanoTime();
    	
    	System.out.println("--------------------------");
    	
    	long start2 = System.nanoTime();
    	Scanner scannerTest = new Scanner(new FileReader("c:\\speed.txt"));
    	while(scannerTest.hasNext()) {
    		System.out.println(scannerTest.next());
    	}
    	long end2 = System.nanoTime();

      결과
      BufferedReader와
      Scanner의 
      속도비교
      --------------------------
      BufferedReader와
      Scanner의
      속도비교

      BufferedReader실행시간:688000
      Scanner실행시간:1857200
   ```
   실행할 때마다 다른 값을 가져오긴 하는데 대략 2~3배정도 BufferedReader가 빠른 거 같습니다.  
   <br>
   2)BufferReader와 Scanner 숫자처리
   숫자를 사용하기 위해서 BufferReader는 __문자열__ 만 받기 때문에 숫자를 사용하기 위해선 파싱을 해줘야 하지만 Scanner는 기본타입을 전부 입력받을 수 있기 때문에 더 활용적입니다.   
   <br>
1. # BufferedReader의 read(), readLine()
   1)read()   
   첫 글자만 아스키코드 값으로 받아서 10진수 int형으로 저장합니다.
   ```java
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

      int bufferRead = br.read(); //k입력   
      System.out.println(bufferRead); //'k'의 아스키코드값 107출력
   ```
   문자를 그대로 받기 위해선 형변환을 해주고 숫자를 그대로 받아오기 위해선 문자-'0'을 해줍니다.
   ```java
      int bufferRead = br.read(); //k입력   
      System.out.println((char)bufferRead); //'k'출력

      int bufferRead2 = br2.read(); // 98입력
      System.out.println(bufferRead2-'0'); // 제일 앞자리 9출력
   ```   
   2)readLine()   
   문자열을 한 줄 끝까지 개행문자(\r\n)포함 입력받고 개행문자는 버립니다. 전체 글자 길이에 공백도 포함됩니다.
   ```java
      String bufferReadLine = br.readLine(); //ab cde fg입력
      System.out.println("bufferStr:"+bufferReadLine+" ,length:"+bufferReadLine.length());
      
      결과
      bufferStr:ab cde fg ,length:9
   ```
   숫자로 입력받기 위해선 파싱을 해줍니다.
   ```java
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));   
      
      int brInt = Integer.parseInt(br.readLine());
    	float brFloat = Float.parseFloat(br.readLine());
    	double brDouble = Double.parseDouble(br.readLine());
   ```   
   <br>
1. # Scanner의 next(), nextLine()
   1)next()   
   공백을 만날 때까지 한 문장을 입력 받습니다. 뒤에 개리지 리턴값은 그대로 남겨놓습니다.
```java
   String scannerNext = scanner.next(); //ab cde fg입력
   System.out.println("scannerNext:"+scannerNext+ " ,length:"+scannerNext.length()); //공백을 만날 때까지 첫 문장인식

   결과
   scannerNext:ab ,length:2 
```
   2)nextLine()
   문자열을 한 줄 끝까지 개행문자(\r\n)포함 입력받고 개행문자는 버립니다.
```java
   String scannerNextLine = scanner.nextLine(); //
   System.out.println("scannerNextLine:"+scannerNextLine+" ,length:"+scannerNextLine.length());

   결과
   scannerNextLine:ab cde fg ,length:9
```   
<br>
1. # 개행문자  
   줄바꿈 문자 \n (LF : 아스키코드10-라인피드)
   줄의 시작위치로 이동 \r (CR : 아스키코드13-캐리지리턴)
   윈도우:CRLF \r\n
   유닉스 계열:LF \n
   맥(macOS 9 이전버전):CR \r
