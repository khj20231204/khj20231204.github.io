---
layout: single
title: JDK와 이클립스 설치
categories: Ubuntu
tag: 
---

1. # JDK설치
   구글에서 JDK검색   
   <img src="../../imgs/ubuntu/jdk.png" style="border:3px solid black;border-radius:9px;width:800px">   

   자바 스프링 3버젼을 사용하기 위해서는 최소 JDK 17버젼 이상을 사용해야 합니다.   
   JDK 17을 선택하고 x64 Compressed Archive를 다운 받습니다.   
   <img src="../../imgs/ubuntu/jdk.png" style="border:3px solid black;border-radius:9px;width:800px">   

   일반적으로, 사용자 프로그램은 usr디렉토리에 저장하므로 usr디렉토리에 java라는 디렉토리를 만들어 다운받은 파일을 이동 후 압축을 해제합니다.   
   ```cs
      //java 디렉토리 만들기
      ubuntu22@ubuntu22-16Z95P-GA76K:~$ cd /usr
      ubuntu22@ubuntu22-16Z95P-GA76K:/usr$ sudo mkdir java
      
      //java 디렉토리로 다운받은 파일 이동
      ubuntu22@ubuntu22-16Z95P-GA76K:/home$ cd /home/ubuntu22/다운로드
      ubuntu22@ubuntu22-16Z95P-GA76K:~/다운로드$ sudo mv jdk-22_linux-x64_bin.tar.gz /usr/java
      
      //압축 해제
      buntu22@ubuntu22-16Z95P-GA76K:/usr/java$ sudo tar zxvf jdk-22_linux-x64_bin.tar.gz 
   ```   

   
