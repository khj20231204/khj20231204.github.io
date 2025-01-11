---
layout: single
title: 우분투 IntelliJ 설치
categories: Ubuntu
tag: 
---

1. # IntelliJ 설치
   <a href="https://www.jetbrains.com/idea/download/?var=1&section=linux">https://www.jetbrains.com/idea/download/?var=1&section=linux</a>   
   tar.gz 파일 다운   

   ```yml
      sudo mkdir ideaIU   # ideaIU 디렉토리 생성
      sudo mv ideaIU-2024.3.1.1.tar.gz ./ideaIU/   # IntelliJ파일 ideaIU 디렉토리로 이동
      cd ideaIU   # ideaIU 디렉토리로 경로 이동
      sudo tar zxvf ideaIU-2024.3.1.1.tar.gz      # 압축 풀기
   ```
   <img src="../../imgs/ubuntu/idea_2.png" style="border:3px solid black;border-radius:9px;width:700px">   
   압축을 풀면 디렉토리가 새로 생성됨   
   
   ```yml
      cd bin    # bin 디렉토리로 이동
      ./idea.sh    # 실행
   ```