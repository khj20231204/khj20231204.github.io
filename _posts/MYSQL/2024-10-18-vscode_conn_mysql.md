---
layout: single
title: VS Code에서 MySQL 연결
categories: MYSQL
tag: []
author_profile: false
---
 
1. # 확장 팩 설치
   Extension 설치   
   <img src="../../imgs/mysql/extension_mysql.png" style="border:3px solid black;border-radius:9px;width:500px">   

   connection 만들기   
   <img src="../../imgs/mysql/extension_mysql2.png" style="border:3px solid black;border-radius:9px;width:500px">   

   아이디, 비번, 데이터베이스명을 입력 후 하단에 Connect 클릭   
   <img src="../../imgs/mysql/extension_mysql3.png" style="border:3px solid black;border-radius:9px;width:500px">   
   입력 값들을 save 해놓을 수도 있습니다.   

   왼쪽 Explorer 탭에서 연결 확인   
   <img src="../../imgs/mysql/extension_mysql4.png" style="border:3px solid black;border-radius:9px;width:500px">   

   연결이 되면 기존 프로젝트의 sql확장자 파일에 다음과 같은 실행 커멘트가 자동으로 나타납니다.   
   <img src="../../imgs/mysql/extension_mysql5.png" style="border:3px solid black;border-radius:9px;width:500px">   

1. # VS Code에서 바로 쿼리 작성
   VS Code에서 MySql과 연동하여 바로 쿼리를 작성하기 위해서 db에 연결을 합니다.   

   user.sql 파일의 상단에 Active Connection을 클릭합니다.   

   추천 항목으로 다음과 같은 항목이 뜨면 차례로 선택합니다.   
   <img src="../../imgs/mysql/extension_mysql7.png" style="border:3px solid black;border-radius:9px;width:700px">  
    
   MySQL_membersdb -> membersdb  

   연결된 것을 확인 할 수 있습니다.
   <img src="../../imgs/mysql/extension_mysql8.png" style="border:3px solid black;border-radius:9px;width:700px">  