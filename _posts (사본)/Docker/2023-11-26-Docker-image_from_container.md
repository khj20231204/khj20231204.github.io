---
layout: single
title: 컨테이너로부터 이미지 작성
categories: Docker
tag: []
---

1. # 컨테이너로부터 이미지 작성
   ```s
      docker container commit [옵션] 컨테이너명 이미지명[:태그명]
   ```   

   |   옵션   |   설명   |
   |:--------:|:--------:|
   |--author, -a|작성자 지정|
   |--=message, -m|메시지 지정|
   |--change, -c|커밋시 Dockerfile 명령을 지정|
   |--pause, -p|컨테이너를 일시정지하고 커밋|

   예)   
   ```s
      root@ubuntudesk:/home/ubuntu-desk# docker container ls
      CONTAINER ID   IMAGE  COMMAND   CREATED      STATUS     PORTS   NAMES
      087580992b39   nginx  "/docker-entrypoint.…" 52 minutes 80/tcp  new_nginx

      root@ubuntudesk:/home/ubuntu-desk# docker container commit -a "name_kim" new_nginx name_kim_image:1.0
      sha256:bcd903496782acfbb50d6828c67d5e435d7c891101de535de60f30bf4b4c1562
      
      root@ubuntudesk:/home/ubuntu-desk# docker images
      REPOSITORY       TAG       IMAGE ID       CREATED         SIZE
      name_kim_image   1.0       bcd903496782   7 seconds ago   187MB
      nginx            latest    a6bd71f48f68   5 days ago      187MB
   ```   
   docker container commit -a "name_kim" new_nginx name_kim_image:1.0   
   -a : 작성자를 name_kim으로 합니다. docker image inspect에서 확인 가능 "Author": "name_kim"   
   new_nginx : 이미지화할 컨테이너 이름   
   name_kim_image : 새로 만들 이미지명   
   1.0 : 태그로 적고싶은 내용을 적지만 보통 버전을 적음   

1. # export/import 와 save/load
   
   도커에서 export와 save는 이미지를 내보내는 두 가지 다른 방법입니다.

   docker export: 컨테이너의 파일 시스템을 tar 아카이브로 내보냅니다. 이 명령어를 사용하면 컨테이너의 파일 시스템만을 내보내며, 컨테이너의 설정, 환경 변수, 이미지의 레이어 등은 포함되지 않습니다. 따라서 다른 도커 환경에서 이미지를 다시 빌드하거나 공유하기 위해서는 docker import 명령어를 사용해야 합니다.   
   docker export 컨테이너ID > 파일명.tar

   docker save: 이미지와 해당 이미지의 모든 레이어를 tar 아카이브로 내보냅니다. 이 명령어를 사용하면 이미지의 설정, 환경 변수, 레이어 등 모든 정보가 포함됩니다. 따라서 다른 도커 환경에서 이미지를 불러오거나 공유할 수 있습니다.   
   docker save 이미지이름 > 파일명.tar   

   요약하면, export 명령어는 컨테이너의 파일 시스템만을 내보내는 반면, save 명령어는 이미지와 해당  이미지의 모든 레이어를 내보냅니다.

1. # 컨테이너를 tar파일로 출력 - export
   가동 중인 컨테이너의 디렉토리/파일들을 모아서 tar 파일을 만들 수 있습니다. 이 tar파일을 바탕으로 하여 다른 서버에서 컨테이너를 가동시킬 수 있습니다.
   ```s
      docker container expoer 컨테이너명/컨테이너ID > 타르명.tar
   ```   

   예)
   ```s
      root@ubuntudesk:/mydir# docker container ls
      CONTAINER ID   IMAGE  COMMAND               PORTS     NAMES
      087580992b39   nginx  "/docker-entrypoint"  80/tcp    new_nginx

      root@ubuntudesk:/mydir# docker container export new_nginx > new_nginx.tar

      root@ubuntudesk:/mydir# ls
      chown_ex  new_nginx.tar

      tar내용 확인:
      root@ubuntudesk:/mydir# tar -tf new_nginx.tar
      .dockerenv
      bin
      boot/
      dev/
      dev/console
      dev/pts/
      dev/shm/
      docker-entrypoint.d/
      ...
   ```   
   docker container export new_nginx > new_nginx.tar   
   new_nginx : tar롤 만들 컨테이너 이름   
   `>` : 리다이렉트   
   new_nginx.tar : tar명   

1. # tar파일로부터 이미지 작성 - import
   ```s
      docker image import <파일 또는 URL> | 이미지명[:태그명]
   ```
   압축된 디렉토리나 파일도 가능   
   지정할 수 있는 파일은 하나뿐이라 tar로 압축 후 실행

   ```s
   root@ubuntudesk:/mydir# cat tar_ex.tar | docker image import - tar_ex_image:1.0
   sha256:379953565739fe002a3f3e125dc5f0323d78621db4d2f9ddd9d2032c95329059
   ```   

1. # 이미지를 tar파일로 저장 - save
   ```s
      docker image save [옵션] 만들tar파일명  저장할이미지명
      또는
      docker save 이미지이름 > 파일명.tar
   ```   

   예)image_ex라는 이미지를 image_ex.tar에 저장   
   ```
      docker image save -o image_ex.tar image_ex
   ```
   -o : 저장할 파일명 지정


1. # tar파일 이미지 읽어 들이기 - load
   tar 이미지로부터 이미지를 읽어 들일 수 있습니다.   
   ```
      docker image load [옵션]
   ```   

   예)export.tar라는 이름의 이미지를 읽어 들임
   ```
      docker image load -i export.tar
   ```   



