---
layout: single
title: 07_24.오라클 설치
categories: JAVA(Lesson)
tag: []
author_profile: false
---

1. # 오라클 설정
   Oracle을 다운 받아서 설치하면 경로는 자동 설정이 됩니다.   
   <img src="../../../imgs/LESSON/SQL(Lesson)/oracle_path.png" style="border:3px solid black;border-radius:9px;width:800px">   

   Oracle을 설치하면 서비스에 5개의 서비스가 생성되는데 
   OracleServiceXE와 OracleXETNSListener이 가장 중요한 서비스입니다.   
   <img src="../../../imgs/LESSON/SQL(Lesson)/service_oracle.png" style="border:3px solid black;border-radius:9px;width:800px">   

1. # cmd에서 오라클 계정접근

   DBA 계정 : sys, system   
   교육용 계정 : scott, hr   

   ```js
      C:\Users\user>sqlplus system/oracle

      SQL*Plus: Release 11.2.0.2.0 Production on 수 7월 24 16:51:02 2024

      Copyright (c) 1982, 2014, Oracle.  All rights reserved.
      Connected to:
      Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production

      SQL> show user    //현재 접속 계정
      USER is "SYSTEM"
      
      SQL> select * from tab;  //table가져오기
      SQL> connect system/oracle  //계정 변경
      Connected.
      
      SQL> show user       
      USER is "SYSTEM"
      
      SQL> conn sys/oracle as sysdba
      Connected.
      
      SQL> show user
      USER is "SYS"
   ```   
   system보다 sys가 상위 계정이기 때문에 sys로 접속시   
   'as sysdba'를 입력해줘야 합니다.   

1. # scott계정 활성화
   


   