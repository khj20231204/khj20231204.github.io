---
layout: single
title: 명령어(사용자,그룹)
categories: Ubuntu
tag: [초기root, useradd, passwd, su, usermode, userdel, users, who, passwd, groupadd, groupdel, groupmode]
---

1. # 초기 root 암호
   기본적으로 root 계정의 암호는 공백이거나 설정되어 있지 않습니다. 따라서 초기에는 root 계정에 암호가 없으며, 로그인할 수 없습니다. 이를 통해 시스템 보안을 강화할 수 있습니다.

   1)일반 사용자로 로그인합니다.
   2)sudo passwd root로 설정
   ```
      $ sudo passwd root
      새 암호: 
      잘못된 비밀번호: 암호는 8 개의 문자 보다 짧습니다
      새 암호 다시 입력: 
      passwd: 암호를 성공적으로 업데이트했습니다
      $ su root
      암호: 
      root@root#
   ```

1. # 사용자   
   2. ## 사용자 생성 명령어   
      3. ### useradd   
         계정을 생성하는 명령어로 adduser와 동일   
         계정자의 홈 디렉토리는 '/home/계정명'입니다.   
         생성된 계정 정보는 /etc/passwd, /etc/shadow, /etc/group에 저장   
         ```
            [root@localhost home]# useradd nati2
         ```   

      3. ### passwd   
      생성된 계정자의 패스워드를 입력 및 변경하는 명령어   
      생성된 계정자의 패스워드는 /etc/shadow 안에 기록   

      passwd 계정명 : 암호 지정   
      ```
         [root@localhost home]# useradd nati2
         [root@localhost home]# passwd nati2
         Changing password for user nati2.
         New password: 
         Retype new password: 
         passwd: all authentication tokens updated successfully.
      ```   
      useradd로 사용자를 추가한 후 바로 passwd로 암호 설정.   

      passwd [옵션] 계정명   
      -S : 계정 상태 표시   
      (PS:정상, NP:패스워트가 없음, LK:Lock)   
      -d : 계정 패스워드 삭제    
      -u : 계정 lock 상태 해제   

      useradd로 사용자를 생성하면 passwd가 LK상태로 나옵니다.   
      ```
         [root@localhost home]# useradd nati2
         [root@localhost home]# passwd -S nati2
         nati2 LK 2023-08-31 0 99999 7 -1 (Password locked.)
      ```   
      <br>
      
      패스워드를 삭제한 후 -S 상태는 NP.   
      ```
         [root@localhost home]# passwd -d nati2
         Removing password for user nati2.
         passwd: Success
         [root@localhost home]# passwd -S nati2
         nati2 NP 2023-08-31 0 99999 7 -1 (Empty password.)
      ```   
      <br>

      패스워드를 새로 설정한 후 -S 상태는 PS.   
      ```
         [root@localhost home]# passwd nati2
         Changing password for user nati2.
         New password: 
         Retype new password: 
         passwd: all authentication tokens updated successfully.
         [root@localhost home]# passwd -S nati2
         nati2 PS 2023-08-31 0 99999 7 -1 (Password set, MD5 crypt.)
      ```   

      3. ### su
         su : switch user의 줄임말   
         현재 사용자에서 로그아웃하지 않고 다른 사용자의 계정으로 로그안하여 그 사용자의 권한을 획득하는 명령어   
         <br>

         |옵션|설명|
         |:----:|:----:|
         |-, -ㅣ, --login|지정한 사용자의 환경변수를 작용하여 로그인|
         |-s|지정된 셀로 로그인|
         |-c|셀을 실행하지 않고 명령어 실행|

         <br>   
         su - root : 루트 계정으로 로그인   
         
   2. ## 사용자 계정 관리
      3. ### usermode
         /home에 위치한 사용자들의 정보를 변경하는 명령어   
         사용자의 홈 디렉토리 병경, 그룹 변경, 유효기간 등을 변경   

      3. ### userdel
         계정 정보를 삭제   
         옵션없이 userdel을 사용하면 /etc/passwd, /etc/shadow, /etc/group에서 해당 계정의 정보 삭제   
         ```
            [root@localhost nati2]# userdel -r nati2
            userdel: user nati2 is currently used by process 4777    "process가 nati2를 사용하고 있는 경우"

            [root@localhost nati2]# ps aux | grep nati2
            root       4776  0.0  0.1 194112  2480 pts/0    S    07:53   0:00 su nati2
            nati2      4777  0.0  0.1 116324  2912 pts/0    S+   07:53   0:00 bash      "<-- nati2"
            root       5101  0.0  0.1 194112  2500 pts/1    S    08:00   0:00 su nati2
            nati2      5102  0.0  0.1 116324  2912 pts/1    S    08:00   0:00 bash      "<-- nati2"
            root       7306  0.0  0.0 112812   964 pts/1    S+   09:08   0:00 grep --color=auto nati2

            [root@localhost nati2]# kill -9 4777
            [root@localhost nati2]# kill -9 5102

            [root@localhost nati2]# userdel -r nati2
         ```   
         userdel 사용시 -r 을 붙이지 않으면   
         ```
            [root@localhost home]# useradd nati2
            Creating mailbox file: File exists
         ```   
         다음과 같은 오류가 나는데 다시 userdel -r nati2 로 삭제해 주면 됩니다.   
   
         ps [옵션]   
         a : 실행 중인 모든 프로세스   
         u : 사용자 이름과 프로세스 시작 시간 추가   
         x : 실행 중인 프로세스 뿐만 아니라 모든 프로세스   

      3. ### change
         패스워드의 만료 정보를 변경   

   2. ## 사용자 조회
      3. ### users
         시스템에 로그인한 사용자 정보 출력   

      3. ### who  
         현재 시스템에 접속해 있는 사용자 조회   
         사용자 계정명, 터미널 정보, 접속 시간, 접속한 서버 정보 등을 확인가능   
         관리자 root와 일반 사용자 모두 사용 가능   
         *명령어 'who am i' 또는 'whoami'는 자신의 정보를 조회   

         ```
            who | wc -l   '접속자 수' 
         ```   

      3. ### id
         사용자 계정의 uid, gid, group을 확인하는 명령어  

      3. ### w
         현재 접속 중인 사용자 정보를 나타내는 명령어   
         서버의 현재 시간정보, 서버 부팅 후 시스템 작동 시간, 서버 접속자의 총 수, 접속자별 서버 평균 부하율, 로그인 시간 정보등을 알 수 있습니다.   

      3. ### whoami
         현재 자신의 계정 확인

      3. ### cat /etc/passwd
         시스템에 등록된 모든 사용자 계정 정보를 보여줍니다. useradd로 생성된 계정은 이 목록에 나타날 것입니다. 각 계정의 정보는 콜론(:)으로 구분되며, 첫 번째 필드가 사용자 이름입니다.

      3. ### 결론
         cat /etc/passwd:모든 사용자 계정 > who:현재 시스템에 로그인한 계정 > whoami:현재 자신 계정   

1. ## 그룹
   2. ## 그룹 관리

      3. ### groupadd
         새로운 그룹 생성 명령어   

      3. ### groupdel
         기존 그룹 삭제   
         그룹 안에 소속되어 있는 계정명이 있을 경우 해당 그룹은 삭제되지 않습니다.   

      3. ### groupmode
         그룹의 설정을 변경하는 명령어   

   2. ## 그룹 조회
      1. ### groups
         사용자 계정이 속한 그룹 목록을 확인하는 명령어  

         

         









   