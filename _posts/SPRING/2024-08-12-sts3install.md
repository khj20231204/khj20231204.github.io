---
layout: single
title: STS3 설치
categories: SPRING
tag: []
author_profile: false
---

1. # 설치
   <a href="https://github.com/spring-attic/toolsuite-distribution/wiki/Spring-Tool-Suite-3">https://github.com/spring-attic/toolsuite-distribution/wiki/Spring-Tool-Suite-3</a>   
   STS3를 다운 받습니다.   

   다운 받으면 spring-tool-suite-3.9.18.RELEASE-e4.21.0-win32-x86_64.zip란 압축파일이 생깁니다.  
   <img src="../../imgs/spring/sts3_install_1.png" style="border:3px solid block;border-radius:9px;width:600px">   

   오른쪽 마우스를 클릭해 연결 프로그램에서 "Window 탐색기"를 클릭해 내부로 들어가면 sts-bundle이란 폴더가 나옵니다. 다시 해당 폴더 안으로 들어가면 sts-3.9.18.RELEASE란 폴더가 있는데 해당 폴더를 바로 C드라이브로 드래그&드롭하면 압축이 해제됩니다.   
   <img src="../../imgs/spring/sts3_install_2.png" style="border:3px solid block;border-radius:9px;width:600px">   

   sts-3.9.18.RELEASE란 폴더가 C드라이브에 생기고 실행은 STS.exe로 하면됩니다.   
   <img src="../../imgs/spring/sts3_install_3.png" style="border:3px solid block;border-radius:9px;width:600px">   

1. # 프로젝트 생성
   Create new spring Starter Project와 Spring Legacy Project가 있는데   
   Create new spring Starter Project는 스프링 부트 프로젝트를 생성하고,   
   Spring Legacy Project는 스프링 프로젝트를 생성합니다.   

   Spring Legacy Project를 선택합니다.   

   Spring MVC Project를 선택합니다.
   <img src="../../imgs/spring/sts3_install_6.png" style="border:3px solid block;border-radius:9px;width:600px">   

   Spring MVC Project가 화면에 없는 경우   
   1)Configure templates 목록 삭제   
   Configure templates를 선택합니다.   
   <img src="../../imgs/spring/sts3_install_4.png" style="border:3px solid block;border-radius:9px;width:600px">   

   spring-data-gemfire와 spring-integration 2개 파일을 remove로 제거를 합니다.   
   <img src="../../imgs/spring/sts3_install_5.png" style="border:3px solid block;border-radius:9px;width:600px">   

   2)xml 파일 추가
   STS3의 workspace경로\.metadata\.plugins\org.springsource.ide.eclipse.commons.content.core 를 선택합니다.   
   ex)C:\Users\user\Documents\workspace-sts-3.9.18.RELEASE\.metadata\.plugins\org.springsource.ide.eclipse.commons.content.core   
   해당 경로에 https-content.xml을 넣습니다.   

