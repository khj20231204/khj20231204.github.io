---
layout: single
title: dockerfile이란
categories: Docker
tag: [이미지 레이어]
---

1. # Dockerfile이란?

   도커파일 → 이미지 생성 ↔ 컨테이어 생성 → 컨테이너 실행   

   컨테이너에서 이미지 만들기    
   베이스가 되는 이미지를 바탕으로 각종 미들웨어나 애플리케이션을 설치하기 위한 일련의 과정을 텍스트 파일로 기술하여 Docker의 인프라 구성을 쉽게 만들기 위해 실행 순서와 정보를 적어놓은 파일입니다.   

1. # 기본 명령어
   대소문자 상관없지만 관례로 대문자를 씁니다.   

   |    명령    |      설명     |
   |:----------:|:-------------:|
   | FROM | 베이스 이미지 지정|
   | RUN | 명령 실행 |
   | CMD | 컨테이너 실행 명령 |
   | LABEL | 라벨 설정 |
   | EXPOSE | 포트 설정 |
   | ENV | 환경변수 |
   | ADD | 파일/디렉토리 추가 |
   | COPY | 파일 복사 |
   | VOLUME | 볼륨 마운드 |
   | USER| 사용자 지정 |
   | WORKDIR | 작업 디렉토리 |
   | SHELL | 기본 쉘 지정 |
   
   `#` : 주석으로 사용   

1. # Dockerfile 작성
   
   __*명령어 앞에 sudo 적으면 에러 발생__   

   ```s
      FROM ubuntu:latest
      
      LABEL title="DockerImage"
      LABEL name="dockerLinux"
      LABEL purpose="practice"

      #도커 내부에 진입시 
      WORKDIR /var/workdir

      #ADD 연습용 - workdir에 sources.list파일 추가
      ADD sources.list /var/workdir/

      #RUN 명령어 연습용 - sources.list를 /etc/apt/에 복사
      RUN cp /var/workdir/sources.list /etc/apt/
      RUN apt update && apt upgrade -y 
   
      #아파치 설치하고 80포트 열고 백그라운드로 실행
      RUN apt-get install apache2 -y  
      EXPOSE 80
      CMD apachectl -DFOREGROUND    ☞애플리케이션 실행

      #쉘 실행 연습용
      RUN ["/bin/bash","-C","echo hello >> test2.html"]
      
      #사용자 계정 생성
      RUN useradd -m dockerLinux
      USER dockerLinux
      RUN ["whoami"]

      #파일 복사 연습용
      COPY VMware-Player-Full-16.2.5-20904516.x86_64.bundle /var/workdir/
      COPY code_1.84.2-1699528352_amd64.deb /var/workdir/      
   ```   
   2. FROM : 베이스 이미지, Dockerfile 작성시 반드시 한 번 이상 입력    

   2. LABEL : 이미지에 메타 데이터를 추가, docker inspect 명령어로 확인   
   
   2. WORKDIR : 컨테이너 내부 진입시 바로 실행되는 작업 경로의 디렉토리   
   ```s
      root@ubuntudesk:/var/files# docker attach dockerlinux_container
      root@ubuntudesk:/var/workdir# 
   ```  

   2. ADD : 파일이나 디렉토리를 도커 이미지에 추가하는 명령어입니다. ADD 명령어를 사용하여 로컬 파일이나 디렉토리를 도커 이미지 내부로 복사할 수 있습니다. ADD 명령어는 압축 파일을 자동으로 해제하거나 원격 URL에서 파일을 다운로드하는 등의 기능도 제공합니다.   

   2. COPY : 로컬 파일이나 디렉토리를 도커 이미지에 복사하는 명령어입니다. COPY 명령어는 단순히 파일을 복사하고자 할 때 사용됩니다. COPY 명령어는 로컬 파일 시스템 상의 파일을 도커 이미지 내부로 복사하는 기능을 수행합니다.   

   2. ADD와 COPY 차이점 : ADD 명령어는 파일을 다운로드하거나 압축을 해제하는 등의 기능을 제공하지만, COPY 명령어는 단순히 파일을 복사하는 기능만을 제공한다는 것입니다. 따라서 파일을 복사하는 목적이라면 COPY 명령어를, 압축 파일을 해제하거나 원격 URL에서 파일을 다운로드해야 하는 경우에는 ADD 명령어를 사용하는 것이 좋습니다.   

   2. RUN 명령어: RUN 명령어는 도커 이미지 빌드 단계에서 실행되는 명령어입니다. RUN 명령어를 사용하여 도커 이미지 내에서 컨테이너 환경을 설정하고 필요한 패키지를 설치하거나 소스 코드를 빌드하는 등의 작업을 수행할 수 있습니다. RUN 명령어는 도커 이미지를 빌드할 때 한 번 실행되며, 이미지 내부의 변경 사항을 적용하는 데 사용됩니다.   

   2. CMD 명령어: CMD 명령어는 컨테이너가 실행될 때 실행되는 명령어입니다. CMD 명령어를 사용하여 컨테이너가 시작되면 실행할 기본 명령어나 스크립트를 지정할 수 있습니다. CMD 명령어는 Dockerfile에서 마지막으로 실행되는 명령어로, 컨테이너가 시작될 때마다 실행됩니다. 만약 Dockerfile에서 CMD 명령어를 여러 번 사용한다면, 마지막 CMD 명령어만 유효하게 적용됩니다.   

   2. RUN와 CMD 차이점 : RUN은 이미지 빌드 단계에서 실행되는 명령어이고, CMD는 컨테이너가 실행될 때 실행되는 명령어입니다.      

   2. EXPOSE : Dockerfile의 빌드로 생성된 이미지에서 노출할 포트를 설정합니다. 그러나 EXPOSE를 설정한 이미지로 컨테이너를 생성했다고 해서 반드시 이 포트가 호스트의 포트와 바인딩되는 것은 아니며, 단지 컨테이너의 80번 포트를 사용할 것 임을 나타내는 것 뿐입니다.   

   2. USER : 사용자의 계정을 생성하는 명령어로 미리 RUN 명령으로 작성해 놓아야 합니다.   

1. # build나 run명령시 생성되는 파일 위치
   
   ```s
      root@ubuntudesk:/var/lib/docker# ls
      buildkit  containers  engine-id  image  network  overlay2  plugins  runtimes  swarm  tmp  volumes
   ```   
   여기에 containers와 image 디렉토리 안에 컨테이너와 이미지 파일이 생성됩니다.   

   불필요한 캐시 삭제   
   ```s
      docker builder prune
   ```   
   Docker build를 여러 번 실행하면 /var/lib/docker 디렉토리 내부의 캐시가 계속 쌓이게 됩니다. 이는 Docker 이미지가 커지고 디스크 공간을 차지하게 될 수 있습니다. 따라서 불필요한 캐시를 제거하기 위해 필요한 경우 docker builder prune 명령을 사용하여 도커 빌더 캐시를 정리할 수 있습니다.   

1. # multi-stage Dockerfile
   ```s
      # 1. Build Image
      FROM golang:1.13 AS builder

      # Install dependencies
      WORKDIR /go/src/github.com/asashiho/dockertext-greet
      RUN go get -d -v github.com/urfave/cli

      # Build modules
      COPY main.go .
      RUN GOOS=linux go build -a -o greet .

      # ------------------------------
      # 2. Production Image
      FROM busybox  
      WORKDIR /opt/greet/bin

      # Deploy modules
      COPY --from=builder /go/src/github.com/asashiho/dockertext-greet/ .
      ENTRYPOINT ["./greet"]
   ```   

1. # 이미지 레이어
   Dockerfile을 빌드하면 기술된 명령마다 내부 이미지가 하나씩 작성됩니다. 용량을 줄이기 위해서 다음과 같은 방식을 사용합니다.   

   다음은 4개의 레이어가 생깁니다.   
   ```s
      RUN yum -y install httpd
      RUN yum -y install php
      RUN yum -y install php-mbstring
      RUN yum -y install php-pear
   ```
  
   다음은 1개의 레이어가 생깁니다.
   ```s
      RUN yum -y install httpd php php-mbstring php-pear
   ```   

   줄바꿈(`\`)을 사용할 수도 있습니다.   
   ```s
      RUN yum -y install\ 
                  httpd\
                  php\
                  php-mbstring\
                  php-pear
   ```

  
