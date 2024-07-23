---
layout: single
title: dockerfile ADD/COPY
categories: Docker
tag: []
---

1. # ADD명령
   이미지에 호스트 컴퓨터에 있는 파일을 추가할 때 사용하는 명령어입니다. ADD 명령은 호스트상의 파일이나 디렉토리, 원격 파일을 Docker 이미지 안으로 복사합니다.   

   ADD <호스트 파일 경로> <Docker 이미지의 파일 경로>

   예)host.html 파일을 /docker_dir/에 추가   
   ```s
      ADD host.html /docker_dir/
   ```   
   호스트 컴퓨터에 있는 host.html 파일을 이미지가 컨테이너로 생성될 때 새로 만들어지는 /docker_dir 디렉토리에 저장됨   
   /docker_dir은 호스트 컴퓨터의 디렉토리가 아니라 image를 컨테이너로 생성했을 때 그 안에 만들어지는 디렉토리.

   ```s
      # [hos]로 시작하는 모든 파일 추가
      ADD hos* /docker_dir/
   ```   
   

1. # 디렉토리 설정
   Docker 이미지 안에 파일은 절대 경로로 지정하거나 WORKDIR 명령에서 지정한 디렉토리를 기점으로 한 경로로 지정합니다.   
   2. RUN 명령   
   2. CMD 명령   
   2. ENTRYPOINT 명령   
   2. COPY 명령   
   2. ADD 명령   
   사용시 docker는 WORKDIR 디렉토리를 이용하게 됩니다.   
   
   예)WORKDIR에 /docker_dir을 지정한 상태에서, /docker_dir 안에 web이란 디렉토리에 host.html을 복사
   ```s
      WORKDIR /docker_dir
      ADD host.html web/
   ```   

1. # 컨테이너 생성 후 생긴 디렉토리
   ```s
      root@ubuntudesk-virtual-machine:/var/files# docker container run -it --name "whale" c084e878ee6c
      root@1df1ec7b2bed:/var/files2# ls
      exercise.txt
      root@1df1ec7b2bed:/var/files2# pwd
      /var/files2
      root@1df1ec7b2bed:/var/files2# cd ..
      root@1df1ec7b2bed:/var# ls
      backups  cache  files2  lib  local  lock  log  mail  opt  run  spool  tmp
      root@1df1ec7b2bed:/var# docker container ps
      bash: docker: command not found
      root@1df1ec7b2bed:/var# docker info
      bash: docker: command not found
      root@1df1ec7b2bed:/var# 

   
   ```

1. # URL로 파일 추가
   url로 파일이 추가된 경우 해당 파일의 퍼미션은 600(r-x------ : 사용자만 읽고쓰기)이 됩니다. ADD 명령은 인증을 지원하지 않기 때문에 원격 파일의 다운로드에 인증이 필요한 경우 RUN 명령에서 wget 명령이나 curl 명령을 사용해야 합니다.   

   ```s
      ADD http://www.msdn.com/index.aspx /docker_dir/web/
   ```   

   호스트에서 가져온 파일이 tar이거나 압축 포맷일 때는 디렉토리로 압축을 풉니다. 하지만 원격 url로 다운받은 리소스는 압축이 풀리지 않습니다.   

1. # COPY
   이미지에 호스트의 파일이나 디렉토리를 복사할 때 이용
   ```s
      COPY <호스트파일경로> <docker이미지경로>
   ```   
   ADD와 매우 유사한 명령어입니다. ADD 명령은 원격 파일의 다운로드나 아카이브의 압축 해제등과 같은 기능을 갖고 있지만, COPY 명령은 호스트의 파일을 이미지 안에 복사 처리만 합니다. 단순히 이미지 안에 파일을 복사만 하고 싶을 때 COPY명령을 이용합니다.