---
layout: single
title: 명령어(리눅스 일반)
categories: Ubuntu
tag: [우분투 version, ln, which, alias, path, 아키텍쳐, man, whatis, whereis]
---

[nati@localhost ~]$ $이면 일반 사용자 모드   
[root@localhost ~]# #이면 루트 사용자 모드   

1. # 리눅스 명령어  
   2. ## 우분투 version 확인   
      Ubuntu에서 현재 버전을 확인하는 방법은 다음과 같습니다   
      ```s
         lsb_release -a   
      ```
      이 명령어는 Ubuntu의 모든 정보를 표시해줍니다. “Description” 또는 “Release” 항목에서 Ubuntu 버전을 확인할 수 있습니다.   

      또는 다음 명령어를 사용하여 간단히 버전을 확인할 수도 있습니다   
      ```s
         cat /etc/os-release
      ```
      이 명령어는 “/etc/os-release” 파일의 내용을 표시합니다. “VERSION_ID” 항목에서 Ubuntu 버전을 확인할 수 있습니다.
      
   2. ## 자신 계정 확인

      whoami명령어   
      ```s
         root@ubuntudesk-virtual-machine:/home/ubuntu-desk# whoami
         root ☜루트 계정

         ubuntu-desk@ubuntudesk-virtual-machine:~$ whoami
         ubuntu-desk ☜사용자 계정
      ```   
      
      id명령어   
      ```s
         root@ubuntudesk-virtual-machine:/home/ubuntu-desk# id
         uid=0(root) gid=0(root) groups=0(root) ☜루트 계정

         ubuntu-desk@ubuntudesk-virtual-machine:~$ id
         uid=1000(ubuntu-desk) gid=1000(ubuntu-desk) groups=1000(ubuntu-desk),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),122(lpadmin),134(lxd),135(sambashare) ☜사용자 계정
      ```   
      
   2. ## ln
      줄 번호   
      출력 결과에 줄 번호를 매깁니다.   
      ```s
         [root@localhost nati2]# ps aux | head -3
         USER        PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
         root          1  0.0  0.3 128280  7008 ?        Ss   06:32   0:04 /usr/lib/systemd/systemd --system 
         root          2  0.0  0.0      0     0 ?        S    06:32   0:00 [kthreadd]

         [root@localhost nati2]# ps aux | head -3 | nl
         1	USER        PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
         2	root          1  0.0  0.3 128280  7008 ?        Ss   06:32   0:04 /usr/lib/systemd/systemd --system 
         3	root          2  0.0  0.0      0     0 ?        S    06:32   0:00 [kthreadd]
      ```   

   2. ## which    
      명령어의 경로를 확인하는 명령어   
      alias를 보여주는 명령어   

   2. ## alias   
      ● bashrc에 자주 사용하는 명령어를 특정문자로 입력   
      root 계정에서 사용은 root계정 접속 후 vi ~/.bashrc   
      사용자 계정에서 사용은 사용자 계정에서 vi ~/.bashrc 실행   
      root계정과 사용자계정의 home디렉토리가 다르기 때문   
      .bashrc는 각각의 home 디렉토리에 위치함   

      root계정에서 사용   
      ```s
         root@ubuntudesk:/home/ubuntu-desk# cat ~/.bashrc | tail
         #fi
         PS1='\[\033[01;31m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '

         alias d_b='docker build -t exerc_image ./'
         alias d_r='docker run -it --name exerc_container --net host exerc_image'
      ```   
      d_b와 d_r이란 별명으로 각각을 실행   
      *별명과 명령어 사이에 공백을 넣으면 안됨 d_b = 'docker build -t..' (X)   
      공백없이 입력해야 됨 d_b='docker build -t..' (O)   
      
      ```s
         root@ubuntudesk:~# source .bashrc
         root@ubuntudesk:~# alias
         alias d_b='docker build -t exerc_image ./'
         alias d_r='docker run -it --name exerc_container --net host exerc_image'
         alias la='ls -A'
         alias ll='ls -alF'
         alias ls='ls --color=auto'
      ```   
      bashrc 파일을 수정 후 바로 사용하기 위해서 source명령어 실행   
      alias를 입력하면 alias목록 확인 가능   

   2. ## unalias   
      alias 기능 해제   
      unalias -a : 설정된 모든 alias 해제   
      unalias m : m으로 설정된 alias만 해제   

   2. ## PATH   
      환경변수 PATH는 실행 파일들의 디렉토리 위치를 저장해 놓은 환경 변수입니다.      
      명령어를 입력하면 PATH 변수에 저장되어 있는 경로에서 해당 명령어를 찾아 실행합니다.   
        
      ● PATH 추가하기  
      예)$HOME 홈디렉토리 안에 있는 dev 디렉토리 추가   
      1) __.bash_profile 파일 직접 수정__   
      ```s
         [nati@localhost ~]$ vi .bash_profile  
         PATH=$PATH:$HOME/.local/bin:$HOME/bin:$HOME/dev ☜vi에서 직접 수정 
      ```   
      2) __PATH 명령어 이용__   
      ```s
         
         [nati@localhost ~]$ echo $PATH ☜echo $PATH : 지정된 PATH값을 확인합니다(대소문자 구분)
         usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin:
         /bin:/sbin:/home/nati/.local/bin:/home/nati/bin

         [nati@localhost ~]$ PATH=$PATH:$HOME/dev
         usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin:
         /bin:/sbin:/home/nati/.local/bin:/home/nati/bin:/home/nati/dev
      ```   

   2. ## 아키덱쳐 확인 명령어
      amd64 (x86_64): 64비트 x86 아키텍처를 가리키며, 대부분의 현대 컴퓨터에서 사용됩니다. Intel 및 AMD 프로세서를 포함한 대부분의 x86 호환 프로세서에서 사용됩니다.   

      386 (x86): 32비트 x86 아키텍처를 가리키며, 오래된 컴퓨터 시스템에서 사용됩니다. Intel 80386 프로세서를 기반으로 한 x86 호환 프로세서에서 사용됩니다.   

      arm: ARM 아키텍처를 가리키며, 주로 모바일 장치 및 임베디드 시스템에서 사용됩니다. ARM 프로세서는 에너지 효율적이며, 모바일 기기 및 IoT 장치에 많이 사용됩니다.   

      ```
         $ uname -m 
         또는
         $ arch
         또는
         $ lscpu
      ```   

1. # 리눅스 도움말   
   2. ## man   
      명령어들의 메뉴얼을 제공   
      사용법: man [섹션] [옵션] 명령어   

   2. ## info   
      명령어들의 사용방법, 옵션등을 제공     
      man보다 제공되는 명령어가 한정적   
      사용법: info 명령어   

   2. ## whatis   
      명령어에 대한 간략한 설명   
      와전히 키워드가 일치해야만 사용   
      사용법: whatis 명령어   

   2. ## manpath
      man 페이지의 위치 경로를 검색하여 표시해주는 명령어   

   2. ## whereis   
      명령어의 실행 파일 절대 경로, 소스코드, 설정 파일, 매뉴얼 페이지를 찾아 출력하는 명령어   

1. # 기타 명령어
   2. ## cal(calender)
   시스템에 설정된 달력을 출력   

   2. ## date
      시스템의 날짜와 시간을 표시하거나 변경   

   2. ## tty
      현재 사용하고 있는 단말기 장치의 경로명과 파일명을 출력   
      보통 텔넷 등에서 동일한 계정으로 여러 개 로그인한 경우 확인 시 유용   

   2. ## wall
      모든 로그인된 사용자들에게 터미널을 통해 메시지를 전달하는 명령어   

   2. ## write
      해당 사용자에게 메시지를 전달하는 명령어   

   2. ## mesg
      write을 사용해서 들어오는 메시지 수신 여부를 확인하고 제어하는 명령어   

