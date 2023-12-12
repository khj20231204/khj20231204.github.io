---
layout: single
title: javac encoding 에러
categories: JAVA
tag: [BufferedReader, Scanner, 개행문자]
---

코드 내에 한글이 있기 때문입니다.   
 <img style="border: 3px solid black;border-radius:9px;width:680px;" src="../../imgs/java/javac_error.jpg">   
다음과 같이 컴파일시 인코딩을 해주면 됩니다.   
```java
   javac CarExam2.java -encoding UTF8
```