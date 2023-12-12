---
layout: single
title: 설치
categories: Docker
tag: []
---

1. # 명령어
   - 버전 확인   
   ```
      docker version
   ```   
    
   - 실행 환경 확인   
   ```
      docker system info
   ```   

   - 디스크 이용 현황   
   ```
      docker system df
   ```  

   - 도커 정보   
   ```
      # docker info
   ```   
   
   - 도커 위치   
   ```
      # which docker
      /usr/bin/docker
   ```   

   - 실행 중인 도커 프로세스   
   ```
      ps aux | grep docker
   ```

1. # 커널 확인
   커널이 최소 3.10버전 이상을 사용해야 도커 컨테이너를 정상적으로 사용할 수 있습니다.   
   ```
      커널 버전 확인
      # unmame -r
   ```   

1. # Ubuntu
   docker install for ubuntu로 검색
   docker 설치   
   ```s
      $ sudo apt-get update 
      //패키지 목록 업데이트
      
      $ sudo apt-get install ca-certificates curl gnupg  
      //install, curl, ca-certificates(도커 인증), gnupg(전자서명) 설치

      $ sudo install -m 0755 -d /etc/apt/keyrings
      //전자서명(gpg)파일을 저장 할 keyrings디렉토리를 install -m을 통해 755 퍼미션으로 허가권을 변경

      $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
      //curl로 gpg설치

      $ sudo chmod a+r /etc/apt/keyrings/docker.gpg
      //docker.gpg의 허가권을 모두 읽을 수 있게 수정

      $ echo \
         "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
         "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
         sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
      //docker저장소를 우분투 시스템(/etc/apt/sources.list.d) 저장소 관리 목록 docker.list추가

      $ sudo apt-get update
      //apt 업데이트

      $ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
      //실제 도커 설치
   ```   
   *gnupg는 GNU Privacy Guard의 약자로, 공개키 암호화 및 전자 서명을 지원하는 프로그램입니다. 이는 개인 정보를 보호하고 인증을 제공하기 위해 사용됩니다. 주로 암호화된 메시지를 보내고 전자 서명을 생성하여 메시지의 무결성을 보장하는 데 사용됩니다.   
      
   *소스 분석   
   echo: 텍스트를 터미널에 출력하는 명령어입니다.   

   \: 줄 바꿈 문자를 사용하여 텍스트를 여러 줄에 걸쳐 작성할 수 있도록 합니다.   
      
   $(dpkg --print-architecture): 현재 시스템의 아키텍처를 확인하는 명령어입니다. 이 부분은 Docker 저장소에 사용되는 아키텍처를 동적으로 지정하기 위해 사용됩니다.   
      
   $(. /etc/os-release && echo "$VERSION_CODENAME"): 현재 운영 체제의 코드명을 확인하는 명령어입니다. 이 부분은 Docker 저장소에 사용되는 우분투 버전을 동적으로 지정하기 위해 사용됩니다.   
      
   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null: tee 명령어를 사용하여 텍스트를 파일로 저장하는 동시에 터미널에 출력합니다. sudo를 사용하여 관리자 권한으로 실행하고, /etc/apt/sources.list.d/docker.list 파일에 저장합니다. > /dev/null 부분은 터미널 출력을 무시하도록 지정합니다.   
   ```
      root@root:/etc/apt# ls -al
      total 48
      drwxr-xr-x   8 root root  4096 11월 22 23:04 .
      drwxr-xr-x 132 root root 12288 11월 23 11:22 ..
      drwxr-xr-x   2 root root  4096 11월 22 16:57 apt.conf.d
      drwxr-xr-x   2 root root  4096  4월  8  2022 auth.conf.d
      drwxr-xr-x   2 root root  4096 11월 23 09:56 keyrings ☜ docker전자서명 디렉토리
      drwxr-xr-x   2 root root  4096 11월 22 16:56 preferences.d
      -rw-rw-r--   1 root root  2825 11월 22 23:06 sources.list
      drwxr-xr-x   2 root root  4096 11월 23 09:59 sources.list.d ☜도커 패키지 목록 추가
      -rw-r--r--   1 root root  2760 11월 22 23:00 trusted.gpg
      drwxr-xr-x   2 root root  4096 11월 22 23:04 trusted.gpg.d

      root@root:/etc/apt/sources.list.d# ls
      archive_uri-https_download_docker_com_linux_ubuntu-jammy.list  docker.list ☜docker.list 파일 확인

      root@root:/etc/apt/sources.list.d# cat docker.list ☜내용 확인
      deb [arch=amd64 signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu   jammy stable
   ```   

1. # CentOS
   ```
      # yum install -y yum-utils
      # yum-config- manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
      # yum install -y docker-ce
      # systemctl start docker
   ```   


