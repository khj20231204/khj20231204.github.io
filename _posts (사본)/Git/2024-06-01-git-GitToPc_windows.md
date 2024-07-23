---
layout: single
title: Github에서 PC로 가져오기(SSH이용)
categories: Git
tag: [github, 폴더]
---

1. # windows에서 수행   
   2. ## clone   
      ```
         git clone <깃허브 ssh주소>
      ```   
      깃허브에서 ssh주소를 가져온다   
      <img src="../../imgs/git/pc_window_ssh.png" style="border:3px solid black;border-radius:9px;width:800px">    
      
      clone을 하면 해당 깃허브 주소 이름으로 폴더가 생긴다. 
      <img src="../../imgs/git/GitToPc_1.png" style="border:3px solid black;border-radius:9px;width:800px">    
      
      clone만 해도 init, branch, origin까지 설정되어 있고 add, commit까지는 가능

   2. ## config가 설정되어 있지 않으면 config 설정   
      ```s
         git config --global user.name="natista"
         git config --global user.email="natista@gmail.com"
      ```   

   2. ## ssh키 발급받기   
      내 컴퓨터에 퍼블릭 rsa키를 발급받은 후 이 키를 깃허브에 등록하면 계정 접속이 가능
      ```s
         ssh-keygen -t rsa -b 4096 -C "natista99@gmail.com"
      ```   
      <img src="../../imgs/git/GitToPc_2.png" style="border:3px solid black;border-radius:9px;width:800px">   

   2. ## github Deply keys에 추가   
      <img src="../../imgs/git/GitToPc_3.png" style="border:3px solid black;border-radius:9px;width:800px">    

   2. ## push 성공
      <img src="../../imgs/git/GitToPc_4.png" style="border:3px solid black;border-radius:9px;width:800px">    
   
1. # Linux에서 수행
   Windows 설치 후에 우분투에서 clone 하지 않고 D드라이브에 있는 블로그 파일로 리눅스에서 깃허브에 연결

   2. ## git설치   
      ```s
         sudo apt install git
      ```   

   2. ## branch와 origin은 이미 설정되어 있다

   2. ## config 설정    
      *--global 옵션 주의 : 앞에 -- 두개   

   2. ## github deploy keys에 추가
      ssh 발급 받은 후 windows에서 했던 방식대로 github deploy keys에 추가   
      __*ssh 발급 받고 deploy keys로 add 해주면 윈도우와 우분투 2군데에서 접근 가능__   

   2. ## add → commit → push
   