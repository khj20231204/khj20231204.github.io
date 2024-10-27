---
layout: single
title: 환경과 사용한 모듈들
categories: PROJECT
tag: []
author_profile: false
---   

1. # 로그인
   isLogin - true : 로그인, 회원가입   
   isLogin - false : 마이페이지, 로그아웃   

1. # 지도   
   ```
      npm install --save @svg-maps/south-korea
   ```
   node_modules 폴더에 @svg-maps 폴더가 생긴다. 폴더 내부에 있는 south-korea.svg 파일을 public 폴더 내부에 넣어주자.
   ```
      <svg xmlns="south-korea.svg" viewBox="0 0 524 631">
         <path ~~~ />
         <path ~~~ />
         ~~~
      </svg>
   ```
   svg 태그를 만들어주고, 내부에 south-korea.svg의 svg 태그 내부에 있는 모든 path를 복사해서 넣어준다.

   
