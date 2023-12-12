---
layout: single
title: 소유권과 허가권
categories: Ubuntu
tag: [permission,umask]
---
1. # 소유권과 허가권
   ls -l 명령어로 확인 가능합니다.  
   
   리눅스 시스템에 있는 모든 파일과 디렉토리에는 그것을 엑세스할 수 있는 소유자와 그룹에 대한 소유권을 가지며 그러한 파일과 디렉토리에 액세스할 수 있도록 해주는 허가권으로 접근 제한을 할 수 있습니다.  

   소유권은 파일 또는 디렉토리를 소유하는 사용자나 그룹을 나타냅니다. 각 파일이나 디렉토리는 소유자와 그룹에 의해 소유되며, 소유자는 해당 파일이나 디렉토리에 대한 통제 및 수정 권한을 가지게 됩니다. 보통 계정이름으로 표시되거나 어떤 경우에는 UID값으로 표시됩니다.   

   허가권은 파일이나 디렉토리에 대한 액세스 권한을 제어하는 데 사용됩니다. 소유권을 가진 자만이 각 파일 및 디렉토리에 대해 읽기, 쓰기 및 실행의 세 가지 유형의 허가권을 관리합니다. 이러한 액세스 권한은 소유자에 의해 자신, 해당 그룹 및 기타 사용자에게 각각 할당 되며 파일의 내용을 읽거나 수정하거나 실행할 수 있는지 여부를 제어합니다.     

   소유권과 허가권은 파일 및 디렉토리에 대한 보안 및 접근 제어를 위해 함께 사용됩니다. 소유자는 파일의 소유자를 변경하고, 허가권은 파일에 대한 액세스 권한을 변경하는 데 사용됩니다. 이러한 권한은 다중 사용자 환경을 제공하는 리눅스 환경에서 가장 기초적인 접근 통제 방법입니다.   

1. # chown
   소유권 변경
   ```
      //dir1의 사용자와 그룹 소유권이 모두 root
      [nati@localhost ~]$ ls -l
      drwxrwxrwx. 2 root root 23 Aug 21 02:40 dir1     

      //chown을 사용해서 사용자 소유권 변경
      [root@localhost nati]# chown -R nati /home/nati/dir1    
      [root@localhost nati]# ls -l
      drwxrwxrwx. 2 nati root 23 Aug 21 02:40 dir1

      //chown : 를 사용해서 그룹 소유권 변경
      [root@localhost nati]# chown -R :nati /home/nati/dir1     
      [root@localhost nati]# ls -l
      drwxrwxrwx. 2 nati nati 23 Aug 21 02:40 dir1

      //chown . 를 사용해서 사용자의 소유권과 그룹 소유권을 변경
      [root@localhost nati]# chown -R nati.nati2 /home/nati/dir1
      [root@localhost nati]# ls -l
      drwxrwxrwx. 2 nati nati2 23 Aug 21 02:40 dir1
   ```
   옵션 -R을 붙이지 않으면 하위 디렉토리나 파일들의 소유권은 변경되지 않습니다.
   
1. # chgrp 
   그룹 소유권만 변경   
   파일 또는 디렉토리의 그룹 소유자를 변경하는 데 사용됩니다.   

   ```
      chgrp [옵션] 그룹명 파일명 또는 디렉토리명   
   ```   

   옵션   
   -c: 변경된 파일에 대한 메시지를 출력합니다.   
   -f: 오류 메시지를 표시하지 않고 진행합니다.   
   -h: 심볼릭 링크를 따라가지 않고 심볼릭 링크 자체의 그룹 소유자를 변경합니다.   
   -R: 지정한 디렉토리 내의 모든 파일과 서브디렉토리의 그룹 소유자를 변경합니다.   
   –reference=파일명: 다른 파일의 그룹 소유자를 참조하여 변경합니다.   
   –dereference: 심볼릭 링크가 아닌 대상 파일의 그룹 소유자를 변경합니다.   

   chgrp 명령어를 사용하기 위해서는 해당 파일 또는 디렉토리에 대한 적절한 권한이 필요합니다. 소유자 또는 슈퍼유저(root) 권한이 필요할 수 있습니다.   

   *chown의 :와 chgrp 차이
   chgrp과 chown의 그룹 소유자 변경 방법에서 .이나 :의 사용 여부에는 문법적인 차이가 있지만, 실제로 그룹 소유자를 변경하는 데 있어서는 큰 차이가 없습니다.

1. # 기본 설정 권한
   파일 644 rw-r--r--   
   디렉토리 755 rwxr-xr-x   

1. # umask
   파일은 666, 디렉토리는 777에서 not 연산을 수행해서 기본 설정 권한을 결정    
   umask의 기본값 : 022   
   ```
      [root@localhost ex]# umask  
      0022
   ```   
   아무런 옵션없이 umask명령어 만으로 umask확인   

1. # 파일 명령어
   읽기 : cat, head, tail, more, grep, vi편집기 등   
   쓰기 : vi편집기, nano   
   <span style="color:red">편집기에서 읽기 권한은 있는데 쓰기 권한이 없는 경우 - 편집기를 열어서 읽을 수는 있는데 저장이 안 됨.</span>   
   실행 : 파일이름 입력   

1. # 디렉토리 명령어
   *허가권을 간단히 '권한'으로 작성   

   읽기 : ls   
   쓰기 : rm, mv, cp, touch, mkdir,.. 등 디렉토리 안에 파일과 디렉토리를 조작하는 모든 명령어   
   실행 : cd(해당 디렉토리로 이동할 수 있는 권한)   

1. # 권한-심볼릭 모드
   chmod [augo] [+-=] [rwx] [파일명]   
   a : 전체   
   u : 사용자   
   g : group   
   o : other   

   `+` : 권한 부여   
   `-` : 권한 해제   
   `=` : 권한 할당   

   ```
      chmod u+w file   'file의 사용자에게 w권한 부여'
      chmod g-rx file   'group의 rx권한 해제'
      chmod go+rwx file   'group와 other에 rwx권한 할당.
   ``````

1. # 권한-옥텟(8진수) 모드
   0~7까지 숫자로 설정   
   
   ```
      chmod 640 myDir   '디렉토리 권한 rw- r-- --- 으로 변환'
      chmod 541 m yFile    'myFile 권한 r-x r-- --x 로 변환'
   ```
1. # 권한 설정

   root권한으로 디렉토리를 만든 후 other 권한을 변경하면서 사용자 권한으로 접속해 해당 명령을 실행한 표입니다.   

   1)디렉토리(최소권한 x)    

   |other권한=>| r   | w      | x   |
   |:---:|:---:|:------:|:---:|
   |__실행명령어=>__| __ls__  | __touch__  | __cd__  |
   |0    | x  | x  | x  |
   |1    | x  | x  | o  |
   |2    | x  | __x__  | <span style="color:yellow">x</span>  |
   |3    | x  | 0  | 0  |
   |4    | __?__  | x  |  <span style="color:yellow">x</span>  |
   |5    | o  | x  | o  |
   |6    | __?__  | __x__  |  <span style="color:yellow">x</span>   |
   |7    | o  | o  | o  |
 
   디렉토리에 접근 시 r,w가 허가되더라도 x가 허가 되지 않으면 접근이 금지되거나 잘못된 값이 출력됩니다. 디렉토리로 이동을 할 수 있는 권한이 제한되었는데 디렉토리 내용을 보거나 안에 파일을 변경하는 것이 모순되는 결과를 가져오기 때문에 리눅스에서 x를 제한한 상태에선 디렉토리에 접근하는 것에 제한을 두었습니다.

   2)파일(최소권한 r) 

      |other권한=>| r   | w      | x   |
   |:---:|:---:|:------:|:---:|
   |__실행명령어=>__| __cat__  | __vi(저장)__  | __./파일__  |
   |0    | x  | x  | x  |
   |1    | <span style="color:yellow">x</span>  | x  | __x__  |
   |2    | <span style="color:yellow">x</span>  | __w!__  |  x |
   |3    | <span style="color:yellow">x</span>  | __w!__  | __x__  |
   |4    | o | readonly  |  x  |
   |5    | o  | readonly  | o  |
   |6    | o  |  o |  x   |
   |7    | o  | o  | o  |
 
   2, 3  w권한이 주어진 상태에서 vi편집기를 실행하면 기존의 파일 내용이 출력되지 않는데 이건 r권한기 없기 때문에 읽어들일 수 없기 때문입니다. w권한기 있기 때문에 강제 저장은 가능합니다.   
   파일을 실행한다는 건 파일을 읽을 수 있어야합니다. 최소 r 허가 이상여야 x가 가능합니다. 읽기와 실행이 같이 있어야 실행이 됩니다.