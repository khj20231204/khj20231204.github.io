---
layout: single
title: 프로세스
categories: Ubuntu
tag: [process]
---

1. # 프로세스
   메모리에 적재되어 실행되는 프로그램   
   프로세스마다 고유 ID를 가집니다.   
   
1. # 실행형태

   2. Foreground 프로세스     
      사용자와 상호작용   
      화면에 실행되는 보이는 모든 프로세스   
      응용 프로그램, 명령어   

   2. Backgournd 프로세스   
      사용자의 입력에 관계없이 실행되는 프로그램    
      실행은 되지만 화면상에 나타나 않음   
      시스템 프로그램, 데몬   

1. # 명령어   
   2. ps   
      현재 실행 중인 프로세스의 상태 출력   

      |옵션|설명|
      |:---:|:---:|
      |a|현재 실행 중인 모든 프로세스 출력|
      |e|시스템상의 모든 프로세스 정보|
      |u|사용자 이름과 프로세스 시작 시간 출력|
      |x|접속된 터미널과 사용되고 있는 모든 프로세스 출력|
      |f|자세한 정보 출력|   
   
      ```
         [root@localhost nati]# ps -ef
         UID         PID   PPID  C STIME TTY          TIME CMD
         root          1      0  0 22:14 ?        00:00:02 /usr/lib/systemd/systemd --switched-root --system --deserialize 22
         root          2      0  0 22:14 ?        00:00:00 [kthreadd]
         root          4      2  0 22:14 ?        00:00:00 [kworker/0:0H]
         root          6      2  0 22:14 ?        00:00:00 [ksoftirqd/0]
         ...
      ```   
         
      <span style="color:red">*예전 최상위 프로세스는 initd 였지만 현재는 systemd가 최상위 프로세스</span>   

      |옵션|설명|
      |:---:|:---:|
      |UID|프로세스 소유자 ID|
      |PID|프로세스 ID|
      |PPID|부모 프로세스 ID|
      |C|스케쥴링 위한 cpu사용량|
      |STIME|프로세스 시작 시간|
      |TTY|프로세스와 연결된 터미널|
      |TIME|총 cpu 사용시간|
      |CMD|실행 명령|   

   2. pstree   
      실행 중인 프로세스를 트리구조로 나타냅니다.   

   2. top   
      리눅스 시스템의 운영 상태를 실시간 출력, 프로세스 상태 확인   
      종료는 q   
   
      |옵션|설명|
      |:---:|:---:|
      |-d 시간|실기간 화면 출력 시간 지정(초 단위)|
      |-p PID|모니터할 프로세스 ID지정|   

      ```
      [root@localhost nati]# top

      top - 00:29:39 up  2:15,  2 users,  load average: 0.12, 0.08, 0.06
      Tasks: 206 total,   1 running, 204 sleeping,   1 stopped,   0 zombie
      %Cpu(s):  2.1 us,  1.1 sy,  0.0 ni, 96.5 id,  0.0 wa,  0.0 hi,  0.4 si,  0.0 st
      KiB Mem :  3861260 total,  1511476 free,   932132 used,  1417652 buff/cache
      KiB Swap:  3145724 total,  3145724 free,        0 used.  2641804 avail Mem 

      PID   USER  PR  NI    VIRT    RES  SHR  S  %CPU   %MEM     TIM    COMMAND
       22   root   0  -20     0      0     0  S   0.0    0.0   0:00.00    md      
       23   root   0  -20     0      0     0  S   0.0    0.0   0:00.00 ac-poller
       24   root   0  -20     0      0     0  S   0.0    0.0   0:00.00 watchdogd    
       ...
      ```   
         
      |옵션|설명|
      |:---:|:---:|
      |PR|프로세스 우선순위|
      |NI|프로세스 NICE 값|
      |VIRT|가상 메모리 총량|
      |RES|물리적 메모리 사용량|
      |SHR|공유 메모리 총량|
      |S|해당 프로세스 상태 

         |S상태|설명|
         |:---:|:---:|
         |- D|중단 될 수 없는 sleep 상태|
         |- R|실행 중인 상태|
         |- S|휴먼 상태|
         |- T|정지된 프로세스|
         |- Z|좀비 프로세스|
      |
      |%CPU|CPU 사용률|
      |%MEM|메모리 사용률|
      |TIM|CPU 사용시간|
      |COMMAND|프로세스 시작 시간|   
 
1. # sleep
   ```
      [nati@localhost ~]$ sleep 5 &
      [1] 3000
      [nati@localhost ~]$ ps
         PID TTY          TIME CMD
      2889 pts/0    00:00:00 bash
      3000 pts/0    00:00:00 sleep   /* sleep가 실행 중 */
      3007 pts/0    00:00:00 ps

      [nati@localhost ~]$ ps
         PID TTY          TIME CMD
      2889 pts/0    00:00:00 bash
      3021 pts/0    00:00:00 ps
      [1]+  Done           sleep 5   /* 5초 후 종료 */
   ```   
   sleep [시간(초)] : 일정시간 동안 실행을 sleep가 동작을 하고 멈춤.   
   & : 백그라운드로 실행   
   sleep 5 & : 5초가 sleep를 백그라운드로 실행   
 
1. # 프로세스 제어 명령어
   2. 시그널 번호   
      신호값으로 프로세스에게 이벤트 발생을 전달해주는 소프트웨어 인터럽트   
   2. 시그널 리스트 확인   
      kill -l   
   2. 시그널 종류    
      
      |번호|시그널|기본 동작|
      |:---:|:---:|:---:|
      |1|SIGHUP|프로세스 종료없이 초기화|
      |2|SIGINT|명령어 중단, Ctrl+c|
      |9|SILL|프로세스 강제 종료|
      |15|SIGTEGKIRM|terminate, 무시할 수 있는 종료|
     
      *kill -9 : 강제종료 - 커널이 프로세스를 강제종료하기 때문에 저장되지 않은 데이터는 손실   
      &nbsp;kill -15 : 정상종료 - 종료 시킬 작업을 안전하게 저장한 후 프로세스 종료   

   2. 전달 명령어   

      |명령어|설명|
      |:---:|:---:|
      |kill|PID로 프로세스 제어|
      |pkill|프로세스 이름으로 제어(동일한 이름의 프로세스 모두 종료)|   

1. # kill -l
   kill 명령어에서 지원하는 시그널 목록들   

   ```
      [nati@localhost ~]$ kill -l
      1) SIGHUP	 2) SIGINT	 3) SIGQUIT	 4) SIGILL	 5) SIGTRAP
      6) SIGABRT	 7) SIGBUS	 8) SIGFPE	 9) SIGKILL	10) SIGUSR1
      11) SIGSEGV	12) SIGUSR2	13) SIGPIPE	14) SIGALRM	15) SIGTERM
      16) SIGSTKFLT	17) SIGCHLD	18) SIGCONT	19) SIGSTOP	20) SIGTSTP
      21) SIGTTIN	22) SIGTTOU	23) SIGURG	24) SIGXCPU	25) SIGXFSZ
      26) SIGVTALRM	27) SIGPROF	28) SIGWINCH	29) SIGIO	30) SIGPWR
      31) SIGSYS	34) SIGRTMIN	35) SIGRTMIN+1	36) SIGRTMIN+2	37) SIGRTMIN+3
      38) SIGRTMIN+4	39) SIGRTMIN+5	40) SIGRTMIN+6	41) SIGRTMIN+7	42) SIGRTMIN+8
      43) SIGRTMIN+9	44) SIGRTMIN+10	45) SIGRTMIN+11	46) SIGRTMIN+12	47) SIGRTMIN+13
      48) SIGRTMIN+14	49) SIGRTMIN+15	50) SIGRTMAX-14	51) SIGRTMAX-13	52) SIGRTMAX-12
      53) SIGRTMAX-11	54) SIGRTMAX-10	55) SIGRTMAX-9	56) SIGRTMAX-8	57) SIGRTMAX-7
      58) SIGRTMAX-6	59) SIGRTMAX-5	60) SIGRTMAX-4	61) SIGRTMAX-3	62) SIGRTMAX-2
      63) SIGRTMAX-1	64) SIGRTMAX
   ```   

1. # kill 실습
   ```
      /* sleep를 백그라운드로 6개 실행 */
      [nati@localhost ~]$ sleep 1000 &
      [1] 3820
      [nati@localhost ~]$ sleep 1000 &
      [2] 3827
      [nati@localhost ~]$ sleep 1000 &
      [3] 3834
      [nati@localhost ~]$ sleep 1000 &
      [4] 3841
      [nati@localhost ~]$ sleep 1000 &
      [5] 3848
      [nati@localhost ~]$ sleep 1000 &
      [6] 3856

      [nati@localhost ~]$ ps -ef | grep sleep
      nati       3820   2889  0 07:08 pts/0    00:00:00 sleep 1000
      nati       3827   2889  0 07:08 pts/0    00:00:00 sleep 1000
      nati       3834   2889  0 07:08 pts/0    00:00:00 sleep 1000
      nati       3841   2889  0 07:08 pts/0    00:00:00 sleep 1000
      nati       3848   2889  0 07:08 pts/0    00:00:00 sleep 1000
      nati       3856   2889  0 07:08 pts/0    00:00:00 sleep 1000
      nati       3866   2889  0 07:08 pts/0    00:00:00 grep --color=auto sleep

      /* kill로 옵션 없이 3820실행 > Terminated  */
      [nati@localhost ~]$ kill 3820
      [1]   Terminated              sleep 1000

      /* 옵션 term > Terminated */
      [nati@localhost ~]$ kill term 3827
      bash: kill: term: arguments must be process or job IDs
      [2]   Terminated              sleep 1000

      /* 옵션 15 > Terminated */     
      [nati@localhost ~]$ kill -15 3834
      [3]   Terminated              sleep 1000

      /* 옵션 9 > killed */
      [nati@localhost ~]$ kill -9 3841
      [4]   Killed                  sleep 1000

      /* pkill로 sleep란 이름의 프로세스 모두 종료 > Terminated */
      [nati@localhost ~]$ pkill sleep
      pkill: killing pid 3914 failed: Operation not permitted
      [5]-  Terminated              sleep 1000
      [6]+  Terminated              sleep 1000

      [nati@localhost ~]$ ps -ef | grep sleep
      root       3914    683  0 07:09 ?        00:00:00 sleep 60
      nati       3965   2889  0 07:10 pts/0    00:00:00 grep --color=auto sleep
   ```   




