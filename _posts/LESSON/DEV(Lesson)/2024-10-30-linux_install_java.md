---
layout: single
title: JAVA 설치
categories: DEV(Lesson)
tag: []
author_profile: false
---

1. # 리눅스 설치
   ```
      sudo apt-get update
      sudo apt-get install openjdk17-jdk
   ```   
   윈도우는 path를 설정해줘야 하지만, 리눅스는 path가 자동으로 잡힙니다.   

   ```
      khj@a:~$ javac -version
      javac 17.0.12
      khj@a:~$ whereis java
      java: /usr/bin/java /usr/share/java /usr/share/man/man1/java.1.gz
   ```

   path는 기본적으로 /etc/profile 안에 저장됩니다.   

   자바 실행   
   ```
      khj@a:~/exmy$ javac hello.java
      khj@a:~/exmy$ java hello
   ```