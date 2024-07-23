---
layout: single
title: build부터 run까지
categories: Docker
tag: []
---

간단한 Dockerfile을 만들어서 build로 이미지 생성 후 run으로 컨테이너 생성하는데까지 연습   
```s
   root@ubuntudesk:/var/files# cat exercise.txt ☜ exercise.txt 파일 내용 확인
   this is exercise.txt
   1
   2
   3

   root@ubuntudesk:/var/files# cat Dockerfile  ☜ 간단한 Dockerfile 내용 확인
   FROM ubuntu:latest  ☜ 기본 이미지
   WORKDIR /var/workdir  ☜ 컨테이너 생성시 새로운 우분투에 home디렉토리같이 작업할 디렉토리
   ADD exercise.txt /var/files2  
   ☜ 로컬에 있는exercise.txt파일을 새로운 우분투 /var디렉토리에 files2란 이름으로 저장

   root@ubuntudesk:/var/files# docker build -t exerc_image ./  ☜ Dockerfile을 exerc_image란 이름으로 이미지 생성
   [+] Building 1.9s (8/8) FINISHED   docker:default
   => [internal] load build definition from Dockerfile   0.0s
   => => transferring dockerfile: 205B           0.0s
   => [internal] load .                          0.0s
   => => transferring context:                   0.0s
   => [internal] load metadata for docker.io/ibrary/     1.7s
   => [1/3] FROM docker.io/library/ubuntu:latest@sha256:8eab64ab73af936225685bb  0.0s
   => [internal] load build context              0.0s
   => => transferring context:                   0.0s
   => CACHED [2/3] WORKDIR /var/workdir          0.0s
   => [3/3] ADD exercise.txt /var/               0.1s
   => exporting to image                         0.0s
   => => exporting layers                        0.0s
   => => writing image sha256:3a5bef37fad07746cb79ca     0.0s
   => => naming to docker.io/library/exerc_image         0.0s

   root@ubuntudesk:/var/files# docker images  
   REPOSITORY    TAG       IMAGE ID       CREATED          SIZE
   exerc_image   latest    3a5bef37fad0   18 seconds ago   77.8MB ☜ exerc_image란 이름으로 생성된 이미지 확인

   root@ubuntudesk:/var/files# docker run -it --name exerc_container --net host exerc_image 
   ☜ exerc_container란 이름의 컨테이너 생성 후 -it옵션으로 컨테이너 안으로 바로 접속   
   ☜ --net host 현재 호스트 네트워크 환경과 같은 네트워크 환경 사용

   root@9f4f691b26b3:/var/workdir# ls ☜ exerc_container(9f4f691b26b3) 내부. WORKDIR /var/workdir
   root@9f4f691b26b3:/var/workdir# pwd
   /var/workdir
   root@9f4f691b26b3:/var/workdir# cd ..
   root@9f4f691b26b3:/var# ls
   backups  cache  files2  lib  local  lock  log  mail  opt  run  spool  tmp  workdir
   root@9f4f691b26b3:/var# cat files2 ☜ files2가 exercise.txt임을 확인 
   this is exercise.txt
   1
   2
   3

   root@9f4f691b26b3:/var# exit  ☜ 컨테이너 종료
   exit

   root@ubuntudesk:/var/files# docker ps -a ☜ 컨테이너가 종료되어 ps 안에 보이지 않고 ps -a 에 보임
   CONTAINER ID   IMAGE         COMMAND      STATUS    PORTS   NAMES
   9f4f691b26b3   exerc_image   "/bin/bash"  Exited (0) 43     exerc_container

   root@ubuntudesk:/var/files# docker restart exerc_container ☜ 컨테이너 재시작
   exerc_container

   root@ubuntudesk:/var/files# docker ps  ☜ 재시작 후 ps에 보임
   CONTAINER ID   IMAGE         COMMAND       STATUS  PORTS  NAMES
   9f4f691b26b3   exerc_image   "/bin/bash"   Up      43     exerc_container

   root@ubuntudesk:/var/files# docker attach exerc_container  ☜ exerc_container에 재접속

   root@9f4f691b26b3:/var/workdir# ls
   root@9f4f691b26b3:/var/workdir# pwd
   /var/workdir
   root@9f4f691b26b3:/var/workdir# 
```

