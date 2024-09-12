---
layout: single
title: 리눅스에서 react깔기
categories: REACT
tab: 
---

1. # install
  ```cs
      sudo apt-get update
      sudo apt-get upgrade

      sudo apt-get install node.js //node.js설치
      node -v //버전확인

      sudo apt-get install npm //npm 설치
      npm -v //버전확인
   ```

   update를 하지않고 설치를 했다면 node버전이 낮아 업데이트를 하란 글이 나타날 것입니다.   
   업데이트하기   
   ```cs
      //n(노드 버전 관리 플러그인) 설치
      sudo npm install -g n
      
      //lts 버전 설치
      //n에는 [latest:최신버전,lts:lts 버전,n stable : 안정화 버전]이 있다.
      sudo n lts
      
      //노드 버전 확인 
      node -v

      //npm 업그레이드
      sudo npm i -g npm      
   ```   
   만약 old version이 나온다면 터미널을 다시 실행하면 됩니다.   

   이후 react디렉토리로 이동 후   
   ```cs
      npx create-react-app "firstReact"
   ```   

   firstReact디렉토리로 이동 후   
   ```cs
      npm start
   ```


