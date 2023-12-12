---
layout: single
title: 컨테이너 기본 명령어
categories: Docker
tag: []
---

1. # 컨테이너 생성
   image ID로 생성   
   ```s
      docker container create <imageID>
   ```   
   - docker image ls → docker container create `<`imageID`>` → docker container start `<`containerID`>`   
   예제)nginx이미지로 컨테이너 실행   
   ```s
      root@ubuntudesk:~# docker image ls
      REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
      nginx        latest    a6bd71f48f68   4 days ago    187MB  ☜a6bd71f48f68
      mysql        latest    a3b6608898d6   4 weeks ago   596MB
      centos       latest    5d0da3dc9764   2 years ago   231MB

      root@ubuntudesk:~# docker container create a6bd71f48f68  ☜a6bd71f48f68
      b10fe865c75e8ff1d528ec20d188b17c9e33d1081706c75b832d469bc9f450fe

      root@ubuntudesk:~# docker container start b10fe865c75e8ff1d528ec20d188b17c9e33d1081706c75b832d469bc9f450fe  ☜위에서 create한ID
      b10fe865c75e8ff1d528ec20d188b17c9e33d1081706c75b832d469bc9f450fe

      root@ubuntudesk:~# docker container ls
      CONTAINER ID   IMAGE          COMMAND                   CREATED          STATUS         PORTS     NAMES
      b10fe865c75e   a6bd71f48f68   "/docker-entrypoint.…"   28 seconds ago   Up 7 seconds   80/tcp    zen_noyce
   ```   

   - docker container create한 목록 확인하는 방법
   ```
      docker container ls -a
      docker container ps -a
   ```   
   docker container ls나 docker container ps는 현재 가동 중인 컨테이너만 보이지만 -a 옵션을 하게되면 모든 컨테이너 목록이 보입니다.   

1. # 컨테이너 시작   

   |   run    |   start   |
   |:-------:|:--------:|
   |이미지 pull + create + start를 합친 명령어<br>한번에 모두 실행| 컨테이너를 create로 생성 후<br>컨테이너를 가동 시키는 단일 명령어|
   | 뒤에 image 입력 | 뒤에 container ID 입력|

1. # 컨테이너 시작 - run   

   run 뒤에 image명 또는 imageID      

   ```s
      docker container run ubuntu:latest /bin/echo 'hello'
   ```   
   :ubuntu 최신버전을 로컬 이미지에서 검색하고 없으면 저장소에서 다운받고 이후 컨테이너가 이상없이 실행되었다면 echo로 'hello'를 출력함   

   ```s
      docker container run --name webserver -d -p 80:80 nginx
   ```   
   :webserver란 이름으로 컨테이너를 80번 포트를 열고 nginx이미지를 로컬에서 검색하고 없으면 저장소에서 다운받아 실행   

   ```s
      root@ubuntudesk:/var/files# docker images
      REPOSITORY     TAG     IMAGE ID       SIZE
      whale_image    latest  c084e878ee6c   77.8MB
      second_image   latest  f4f60388f2d1   77.8MB
      hello_image    latest  6065a3e10570   77.8MB

      root@ubuntudesk:/var/files# docker container run -it --name "whale" c084e878ee6c
   ```   
   :whale이란 이름의 컨테이너를 생성하는데 가져올 이미지ID는 c084e878ee6c   

1. # 컨테이너 시작 - start
   start + containerID   
   ```s
      docker container start [옵션] <컨테이너 식별자>
   ```

   |   옵션    |    설명   |
   |:---------:|:---------:|
   |--attach, -a | 표준 출력, 표준 오류 출력을 연다.|
   |--interactive, -l| 컨테이너 표준 입력을 연다. |
      
   예)컨테이너 ID가 dfe334effegv를 시작
   ```s
      docker container start dfe334ef
   ```   

1. # 컨테이너 정지
   ```s
      docker container stop [옵션] <컨테이너 식별자>
   ```   
   
   |   옵션   |   설명   |
   |:---------:|:----------:|
   |--time, -t|컨테이너의 정지 시간을 지정(기본값은 10초)|

   예)컨테이너 ID가 dfe334effegv를 2초 후 정지
   ```s
      docker container stop -t 2 def334
   ```   

   __강제 종료__ 는 __kill__   
   ```s
      docker container kill def334
   ```   

1. # 컨테이너 재시작

    ```s
      docker container restart [옵션] <컨테이너 식별자>
   ```   
   
   |   옵션   |   설명   |
   |:---------:|:----------:|
   |--time, -t|컨테이너의 재시작 시간을 지정(기본값은 10초)|

   예)컨테이너 ID가 dfe334effegv를 2초 후 재시작
   ```s
      docker container restart -t 2 def334
   ```   

 1. # rm와 prune 요약   
   rm도 특정 이미지 1개    
   prune는 이미지 모두 삭제 가능    

1. # 컨테이너 삭제 - rm
   ```s
      docker container rm [옵션] <컨테이너 식별자>
   ```   
   
   |   옵션   |   설명   |
   |:---------:|:----------:|
   |--force, -f|실행 중인 컨테이너를 강제로 삭제|
   |--volumes, -v|할당한 볼륨을 삭제|

   ```s
      docker container rm def334
   ```  
   
1. # 컨테이너 삭제 - prune
   ```s
      $docker container prune
      WARNING! This will remove all stopped containers.
      Are you sure you want to continue? [y/N]
   ```   
   옵션없이 실행하면 전체를 삭제할지 Y/N으로 물어봅니다. Y를 하면 한번에 전체 삭제를 합니다.   

1. # 컨테이너 중단/재개
   ```s
      docker container pause <컨데이너 식별자>

      docker container pasue mysql_ex
   ```  
   mysql_ex컨테이너를 일시 중단시키면 docker container ls 명령으로 확인했을 때 [STATUS]가 (Paused)로 나타납니다.

1. # 컨테이너 상태 확인   
   ```
      docker container ps
   ```   
   컨테이너 자체의 기본정보 ID, 이름, 상태, 포트를 출력

1. # 컨테이너 리소스 확인   
   ```
      docker container stats [컨테이너명]
   ```   
   컨테이너에 할당된 리소스 cpu, 메모리, 네트워크등을 확인   

1. # 컨테이너 목록 표시
   ```
      docker container ls [옵션]
   ```   

   |       옵션     |            설명          |
   |:--------------:|:-----------------------:|
   |--all, -a|실행 중/정지 중인 것도 포함하여 모든 컨테이너를 표시|
   |--filter, -f|표시할 컨테이너의 필터링|
   |--format|표시 포맷을 지정|
   |--last, -n|마지막으로 실행된 n건의 컨테이너만 표시|
   |--no-trunc|정보를 생략하지 않고 표시|
   |--quiet, -q|컨테이너 ID만 표시|
   |--size, -s|파일 크기 표시|
  
   - 컨테이너 목록의 필터링   
   모든 컨테이터를 출력하는데 컨테이너 이름이 'test1'인 것만 출력   
   ```s
      root@ubuntudesk-virtual-machine:~# docker container ls -a -f name=test1
      CONTAINER ID   IMAGE     COMMAND      CREATED        STATUS                    PORTS     NAMES
      ce6496cee5f9   centos    "/bin/cal"   23 hours ago   Exited (0) 23 hours ago             test1
   ```   
   모든 컨테이너를 출력하는데 상태가 exited=0인 것만 출력   
   ```s
      root@ubuntudesk-virtual-machine:~# docker container ls -a -f exited=0
      CONTAINER ID   IMAGE          COMMAND                   CREATED        STATUS                  PORTS  NAMES
      97cda27e4cb7   a6bd71f48f68   "/docker-entrypoint.…"   3 hours ago    Exited (0) 2 hours ago          naughty_goldberg
      0b7869158a9d   nginx          "/docker-entrypoint.…"   4 hours ago    Exited (0) 2 hours ago          laughing_rubin
      7bde08b8a2e9   nginx          "/docker-entrypoint.…"   4 hours ago    Exited (0) 4 hours ago          ex_nginx
      f6f0e92fc3b1   centos         "/bin/bash"               23 hours ago   Exited (0) 23 hours ago        test2
      ce6496cee5f9   centos         "/bin/cal"                23 hours ago   Exited (0) 23 hours ago        test1
      94edc5d009a2   e4c58958181a   "/bin/echo hello-wor…"   2 days ago     Exited (0) 2 days ago           gifted_tesla
      d6ae46bf21b1   9c7a54a9a43c   "/hello"                  2 days ago     Exited (0) 2 days ago          zen_agnesi
   ```   

1. # 컨테이너 이름 변경
   ```
      docker container rename [예전이름] [새이름]
   ```   

   예)ex_nginx를 new_nginx로 변경
   ```s
      root@ubuntudesk:/home/ubuntu-desk# docker container ls
      CONTAINER ID  IMAGE  COMMAND CREATED      STATUS          PORTS   NAMES
      087580992b39  nginx  "/docker-entrypoint" 24 minutes ago  80/tcp  ex_nginx ◀전

      root@ubuntudesk:/home/ubuntu-desk# docker container rename ex_nginx new_nginx

      root@ubuntudesk:/home/ubuntu-desk# docker container ls 
      CONTAINER ID  IMAGE  COMMAND    CREATED    STATUS          PORTS   NAMES
      087580992b39   nginx "/docker-entrypoint"  25 minutes ago  80/tcp  new_nginx ◀후
   ```


