---
layout: single
title: developer연결 시 error
categories: SQL(Lesson)
tag: []
author_profile: false
---   

1. # developer연결 시 error
   sqlplus에서는 접속이 되는데 developer에서 연결 시 에러가 뜨는 경우   
   <img src="../../../imgs/LESSON/SQL(Lesson)/developer_conn_error_1.png" style="border:3px solid black;border-radius:9px;width:700px">   

   서비스에서 oracleXETNSListener를 실행합니다. OracleServiceXE만 실행되어 있어도 sqlplus는 실행됩니다.   
   <img src="../../../imgs/LESSON/SQL(Lesson)/developer_conn_error_3.png" style="border:3px solid black;border-radius:9px;width:600px">   

   OracleServiceXE 서비스가 꺼져있는 경우 sqlplus에서 에러가 발생합니다.   
   <img src="../../../imgs/LESSON/SQL(Lesson)/developer_conn_error_2.png" style="border:3px solid black;border-radius:9px;width:600px">   
   다음과 같은 error가 나타납니다.   

