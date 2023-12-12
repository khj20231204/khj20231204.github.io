---
layout: single
title: 특수권한
categories: Ubuntu
tag: [특수권한,사용자 변경]
---

1. # 특수 권한   
   일반적인 권한과는 조금 다른 특수한 권한   
   - SetUID : 나머지 사용자가 파일을 실행할 때 소유자의 권한으로 접근할 수 있게 해주는 권한.   
   예)rwx r-x --x 의 권한이 있을 때 나머지 사용자의 권한 --x를 소유자의 권한 rwx로 대체    
   - SetGID : 나머지 사용자가 파일을 실행할 때 관리 그룹의 권한으로 접근할 수 있게 해주는 권한.   
   예)rwx r-x --x 의 권한이 있을 때 나머지 사용자의 권한 --x를 그룹의 권한 r-x로 대체    
   - StickyBit : StickBit가 부여된 디렉토리 내에서는 누구나 자신의 파일을 생성, 수정, 삭제 할 수 있지만 다른 사용자의 파일을 수정하거나 삭제할 수는 없습니다. 디렉토리를 마치 자유게시판처럼 사용할 수 있게 해주는 권한입니다. 일반적으로 /tmp 디렉토리가 있습니다.   

   *win+방향키 : 터미널 창 정렬   
   
1. # SetUID
   <table>
      <tr>
         <td>사용자</td>
         <td>그룹명</td>
         <td>소유자</td>
         <td>그룹</td>
         <td>나머지</td>
      </tr>
      <tr>
         <td>root</td>
         <td>mygroup</td>
         <td>rw<span style="color:red;font-style:bold">s</span></td>
         <td>r-x</td>
         <td>소유자 권한</td>
      </tr>
   </table>

   특수권한이 부여된 파일은 __소유자__ 의 권한 부분 중 실행 권한 부분이 x가 아닌 s로 나타납니다.   
   설정 : chmod 4xxx [파일명] 또는 chmod u+s [파일명]   
   ```
      [root@localhost nati]# chmod 4700 file
      [root@localhost nati]# ls -l file
      -rws------. 1 root root 0 Aug 21 00:37 file
   ```   

1. # SetGID   

    <table>
      <tr>
         <td>사용자</td>
         <td>그룹명</td>
         <td>소유자</td>
         <td>그룹</td>
         <td>나머지</td>
      </tr>
      <tr>
         <td>root</td>
         <td>mygroup</td>
         <td>rwx</td>
         <td>rw<span style="color:red;font-style:bold">s</span></td>
         <td>그룹 권한</td>
      </tr>
   </table>      

   특수권한이 부여된 파일은 __그룹__ 의 권한 부분 중 실행 권한 부분이 x가 아닌 s로 나타납니다.   
   설정 : chmod 2xxx [파일명] 또는 chmod g+s [파일명]   
   ```
      [root@localhost nati]# chmod 2700 file
      [root@localhost nati]# ls -l file
      -rwx--S---. 1 root root 0 Aug 21 00:37 file
   ```   
   
1. # StickyBit
   대표적인 예로 /tmp 디렉토리가 있습니다.   

   ```
   [nati@localhost /]$ ls -l
   ...
   drwxrwxrwt.  21 root root 4096 Aug 18 06:12 tmp
   ...
   ```   
   drwxrwxrw<span style="color:red">t</span>. &nbsp; 21 &nbsp; root &nbsp; root &nbsp; 4096 &nbsp; Aug &nbsp; 18 06:12 &nbsp; <span style="color:red">tmp</span>   

   특수권한이 부여된 디렉토리는 __나머지 사용자__ 의 권한 부분 중 실행 권한 부분이 x가 아닌 t로 나타납니다.   

   설정 : chmod 1xxx [디렉토리명] 또는 chmod o+t [디렉토리명]   

   ```
      [root@localhost nati]# chmod 1700 file
      [root@localhost nati]# ls -l file
      -rwx-----T. 1 root root 0 Aug 21 00:37 file
   ```   
   -rwx-----<span style="color:red">T</span>   

   test사용자 생성 후 로그인하는 방법 : root 계정으로 로그인 후 test로 로그인   
   ```
      [root@localhost ~]# whoami
      root
      [root@localhost ~]# useradd test
      [root@localhost ~]# su - test   'root계정은 로그인 없이 다른 계정으로 로그인 가능'
      [test@localhost ~]$ whoami
      test

   ```   
 
1. # 사용예   
   ```
      [root@localhost nati]# find / -perm -4000   'setID를 가진 파일 찾기'
      ...
      /usr/bin/ksu
      /usr/bin/chfn
      /usr/bin/chsh
      /usr/bin/passwd
      /usr/bin/su
      /usr/bin/chage
      ...
      
      [root@localhost bin]# ls -l ksu chfn chsh passwd su chage
      -rwsr-xr-x. 1 root root 73888 Aug  8  2019 chage
      -rws--x--x. 1 root root 23968 Sep 30  2020 chfn
      -rws--x--x. 1 root root 23880 Sep 30  2020 chsh
      -rwsr-xr-x. 1 root root 61320 Sep 30  2020 ksu
      -rwsr-xr-x. 1 root root 27856 Mar 31  2020 passwd
      -rwsr-xr-x. 1 root root 32128 Sep 30  2020 su
   ```   
   find / -perm -4000란?   
   1)find: 찾는다   
   2)/: 범위는 / 전체 범위   
   3)-perm: 권한으로 찾겠다   
   4)-4000: "-"는 '포함하는'이란 뜻, 4000번 권한을 포함하는.   
   만약 '-'없이 그냥 4000이면 권한이 4777(x), 4775(x) 등은 검색되지 않습니다. 딱 4000인 권한만 출력됩니다   
   
   실행결과   
   전부 -rws.. s 권한을 가지고 있습니다. chage, chsh, ksu, passwd, su 파일을 실행할 때는 소유자의 권한을 가지게 됩니다.   

   * /etc/shadow에 사용자의 password가 저장되어 있음.   
   ```
      [root@localhost khj]# ls -l /etc/shadow
      ----------. 1 root root 1308  9월 16 19:35 /etc/shadow
   ```   
   
1. # 실습  
   find perm -4000 결과를 파일에 저장 후 2개의 파일 비교
   ```
      [root@localhost khj]# find / -perm -4000 > original_setuid   /*현재 파일 중 setuid파일 검색, 검색 결과를 파일로 저장*/
      find: ‘/proc/3757/task/3757/fd/5’: 그런 파일이나 디렉터리가 없습니다
      find: ‘/proc/3757/task/3757/fdinfo/5’: 그런 파일이나 디렉터리가 없습니다
      find: ‘/proc/3757/fd/6’: 그런 파일이나 디렉터리가 없습니다
      find: ‘/proc/3757/fdinfo/6’: 그런 파일이나 디렉터리가 없습니다

      [root@localhost khj]# chmod 4700 file  /*file를 setuid파일로 변환*/

      [root@localhost khj]# find / -perm -4000 > make_setuid  /*setuid파일을 생성 후 다시 검색, 검색 결과를 파일로 저장*/
      find: ‘/proc/3795/task/3795/fd/5’: 그런 파일이나 디렉터리가 없습니다
      find: ‘/proc/3795/task/3795/fdinfo/5’: 그런 파일이나 디렉터리가 없습니다
      find: ‘/proc/3795/fd/6’: 그런 파일이나 디렉터리가 없습니다
      find: ‘/proc/3795/fdinfo/6’: 그런 파일이나 디렉터리가 없습니다

      [root@localhost khj]# diff original_setuid make_setuid  /*original_setuid파일과 make_setuid파일을 비교*/
      31a32
      > /khj/file   /*방금 생성한 setuid파일인 file을 찾음*/
   ```