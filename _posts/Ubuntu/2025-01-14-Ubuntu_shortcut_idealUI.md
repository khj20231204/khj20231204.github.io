---
layout: single
title: idealUI 터미널에서 path설정
categories: Ubuntu
tag: 
---

1. # idealUI 터미널에서 path설정

   bashrc파일을 수정
   ```
      sudo vi ~/.bashrc
   ```   

   G를 입력해서 가장 아랫줄로 이동   
   ```yml
      gg  # 첫 행으로 이동
      G  # 마지막 행으로 이동
      u  # 되돌리기
      yy  # 한 줄 복사
      dd  # 한 줄 삭제
      p  # 붙여넣기
   ```  

   현재 path에 경로   
   ```cs
      JAVA_HOME=/usr/local/java/jdk-22.0.1
      JRE_HOME=/usr/local/java/jdk-22.0.1
      PATH=$PATH:$JRE_HOME/bin:$JAVA_HOME/bin
   ```   
   `$`는 변수를 나타냄   
   `$JRE_HOME` => 변수 JRE_HOME를 나타냄   
   `$JAVA_HOME` => 변수 JAVA_HOME를 나타냄   

   IntelliJ bin경로 추가   
   ```cs
      IDEA_HOME=/home/ubuntu22/MyWork/ideaIU/idea-IU-243.22562.218
      PATH=$PATH:$JRE_HOME/bin:$JAVA_HOME/bin:$IDEA_HOME/bin
   ```   

   바로 적용   
   ```cs
      source ~/.bashrc
   ```   

   path 확인   
   ```
      echo $PATH
   ```   

   idea실행   
   ```
      idea.sh
   ```   
   바로 idea.sh를 입력한다 `./idea.sh`가 아님   
