---
layout: single
title: Docker 명령어
categories: Docker
tag: []
---

1. # 컨테이너 재시작

   docker ps에는 보이지 않지만 docker ps -a에 보이면 컨테이너 재시작   
   ```s
      root@ubuntudesk:/var/files# docker ps
      CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

      root@ubuntudesk:/var/files# docker ps -a
      CONTAINER ID   IMAGE         COMMAND       STATUS          PORTS       NAMES
      1df1ec7b2bed   c084e878ee6c  "/bin/bash"   Exited (0) 13 seconds ago   whale
      358e3b18b35b   second_image  "/bin/bash"   Exited (0) 4 days ago       dazzling_ptolemy
   ```   
   STATUS가 Exited가 된 상태   

   ```s
      docker restart [컨테이너 이름 또는 ID]
   ```

   ```s
      root@ubuntudesk:/var/files# docker ps -a
      CONTAINER ID   IMAGE          COMMAND       STATUS     PORTS           NAMES
      1df1ec7b2bed   c084e878ee6c   "/bin/bash"   Exited (0) 13 seconds ago  whale
      358e3b18b35b   second_image   "/bin/bash"   Exited (0) 4 days ago      dazzling_ptolemy

      root@ubuntudesk:/var/files# docker restart whale
      whale

      root@ubuntudesk:/var/files# docker ps
      CONTAINER ID   IMAGE          COMMAND       STATUS  PORTS       NAMES
      1df1ec7b2bed   c084e878ee6c   "/bin/bash"   Up      3 seconds   whale
   ```   
   STATUS가 Up됩니다.

1. # 컨테이너에 재접속
   ```s
      docker attach [컨테이너 이름 또는 ID]
   ```   

   ```s
      root@ubuntudesk-virtual-machine:/var/files# docker attach whale

      root@1df1ec7b2bed:/var/files2# ls   ☜ whale컨테이너에 접속한 상태
      exercise.txt

      root@1df1ec7b2bed:/var/files2# pwd  ☜ Dockerfile의 WORKDIR로 접속 됨
      /var/files2

      root@1df1ec7b2bed:/var/files2# docker info   ☜ 도커 이미지의 새로운 리눅스라 도커가 안깔려있음
      bash: docker: command not found

      root@1df1ec7b2bed:/var/files2# exit  ☜ 빠져나오기
      exit
   ```

1. # 전체 명령어 정리
      
   - 이미지생성
   docker build -t <이미지이름> ./   

   - docker run -it --name <컨테이너이름> --net host <이미지이름>   
   -it : 컨테이터 실행 후 내부 접속   
   --net host : 현재 호스트 네트워크 환경과 같은 네트워크 환경 사용   

   - 실행 중 컨테이너 확인   
   docker container ps   

   - 모든 컨테이너 확인   
   docker container ps -a   

   - 모든 컨테이너 지우기   
   docker container prune   

   - 특정 컨테이너 지우기   
   docker container rm <컨테이너ID or 컨테이너이름>   

   - 모든 컨테이너에서 컨테이너ID 확인 후 재시작   
   docker container restart <컨테이너ID>   

   - 재시작 후 재접속   
   docker attach <컨테이너이름 or 컨테이너ID>   

   - 이미지 확인   
   docker images   

   - 이미지 모두 지우기   
   docker image prune -a   

   - 특정 이미지 지우기   
   docker image rm <이미지ID or 이미지이름>   

   - 현재 컨테이너를 이미지화   
   docker commit <컨테이너 ID> <새로운 이미지 이름>   



