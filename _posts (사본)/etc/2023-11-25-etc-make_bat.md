---
layout: single
title: 배치파일 만들기
categories: etc
tag: []
---

메모장에서

cmd 실행
```s
   @echo 
   cmd.exe
```

cmd창에서 ipconfig 실행
```s
   @echo
   cmd.exe /k "ipconfig"
```

cmd창에서 폴더 이동 후 bundle exec실행
```s
   @echo off
   cmd.exe /c "cd C:\programming\blog\natista99.github.io && bundle exec jekyll serve"
```   

디렉토리에서 명령어 바로 실행
```s
   @echo off
   start /d "C:\Program Files\Google\Chrome\Application" /b chrome.exe
```   
d: 디렉토리 지정   
b: 실행 파일 지정

