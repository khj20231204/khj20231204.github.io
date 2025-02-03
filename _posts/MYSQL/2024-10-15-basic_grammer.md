---
layout: single
title: 기본 문법
categories: MYSQL
tag: []
author_profile: false
---
 
1. # 기본 문법	  

   cmd창에으로 mysql에 접속합니다.   
   ```yml
      명령어  -u[계정명] -p[접속할DB명]
      또는
      명령어  -u [계정명] -p [접속할DB명]
      또는
      명령어  -u [계정명] -p [비밀번호] [접속할DB명]
   ```
   mysql -uroot -p mysql   

   ```js
      show databases;   --데이터베이스 목록
      use sakila;       --데이터베이스 사용
      show tables;      --테이블 목록
      desc testTable;   --testTable 구성

      create database jsptest;    //jsptest라는 데이터베이스 생성
      create user jspid;

      //5.7이하 버전 
      grant all privileges on jsptest.* to jspid@'%' identified by 'jsppass' with grant option;
      //jsptest데이터베이스에 jspid라는 user를 생성하고 jsppass라는 password를 설정하고 권한을 부여
      flush privileges;
      //재시작없이 설정 변경 적용


      //8버전부터
      create user jspid@'%' identified by 'jsppass';
      //jspid라는 user와 jsppass라는 password를 생성
      grant all privileges on jsptest.* to jspid@'%' with grant option;
      //jspid에 권한부여
      flush privileges;
      //재시작없이 설정 변경 적용

      //데이터베이스를 따로 생성해 줘야 합니다.!!!!!
      create database jsptest;
   ```   

1. #  사용자가 존재하지 않는 경우 (새로 생성 필요)

   __root__ 계정으로 실행!

   database : jpa1    
   암호 : 1234   
   사용자 : khj   

   ```sql
      CREATE USER 'khj'@'%' IDENTIFIED BY '1234';
      GRANT ALL PRIVILEGES ON jpa1.* TO 'khj'@'%' WITH GRANT OPTION;
      FLUSH PRIVILEGES;
   ```   

1. # 사용자가 이미 존재하는 경우 (비밀번호 변경 없이 권한만 부여)
   ```sql
      GRANT ALL PRIVILEGES ON jpa1.* TO 'khj'@'%' WITH GRANT OPTION;
      FLUSH PRIVILEGES;
   ```

1. # . 기존 사용자의 비밀번호를 변경하고 싶다면
   ```sql
      ALTER USER 'khj'@'%' IDENTIFIED BY '1234';
      FLUSH PRIVILEGES;
   ```