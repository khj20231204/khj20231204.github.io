---
layout: single
title: 오라클 설치
categories: Ubuntu
tag: 
---

1. # 오라클 설치
   다운 받습니다.   
   <a href="https://www.oracle.com/database/technologies/xe-prior-release-downloads.html">https://www.oracle.com/database/technologies/xe-prior-release-downloads.html</a>

   다운 받은 파일을 압축 풉니다.   

   ```cs   
      oracle-xe-11.2.0-1.0.x86_64.rpm
   ```   

   rpm파일이 있는데 우분투는 데비안 계열이기 때문에 deb로 확장자를 변경해야합니다. 확장자를 변경하기 위해서 alien이란 패키지를 설치합니다.   
   ```cs
      sudo apt install alien
   ```   

   rpm파일을 deb파일로 변환합니다. 3~4분 소요   
   ```cs
      sudo alien --scripts -d oracle-xe-11.2.0-1.0.x86_64.rpm
   ```   

   변환이 완료되면
   ```cs
      ubuntu22@ubuntu22:~/MyWork/Sorftware/oracle-xe-11.2.0-1.0.x86_64.rpm/Disk1$ sudo alien --scripts -d oracle-xe-11.2.0-1.0.x86_64.rpm
      oracle-xe_11.2.0-2_amd64.deb generated
   ```   
   oracle-xe_11.2.0-2_amd64.deb generated와 같이 generated가 뜹니다.   

   __설치하기 전에 환경설정을 먼저__ 해야합니다.   

   환경 설정없이 바로 설치하면 다음과 같은 에러가 발생합니다.   
   <img src="../../imgs/ubuntu/oracle_install_1.png" style="border:3px solid black;border-radius:9px;width:800px">   

   deb파일을 설치합니다.   
   ```
      sudo dpkg --install oracle-xe_11.2.0-2_amd64.deb
   ```

