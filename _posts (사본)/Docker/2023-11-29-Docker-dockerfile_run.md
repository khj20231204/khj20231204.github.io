---
layout: single
title: dockerfile RUN
categories: Docker
tag: [RUN, history]
---

1. # RUN
   Dockerfile 내에서 "애플리케이션을 설치한다", "미들웨어를 설치한다", "환경 설정을 한다" 등의 명령을 실행할 때 RUN명령을 사용합니다.

   ```
      RUN [실행하고 싶은 명령]
   ```   

1. # Shell 형식으로 기술
   명령의 지정을 쉘에서 실행하는 형식을 기술하는 방법입니다.   
   예)apt 명령으로 Nginx를 설치   

   ```
      RUN apt-get install -y nginx
   ```   
   /bin/sh -c 를 사용하여 실행했을 때와 똑같이 작동합니다.   

1. # Exec 형식으로 기술
   Shell 형식으로 명령을 기술하면 /bin/sh 에서 실행되지만, Exec 형식으로 기술하면 쉘을 경유하지 않고 직접 실행합니다. 따라서 명령 인수에 $HOME과 같은 환경변수를 지정할 수 없습니다. Exec 형식은 실행하고 싶은 명령을 JSON배열로 지정합니다.   
   ```
      RUN ["/bin/bash","-c", "apt-get install -y nginx"]
   ```   

1. # 명령어 기술 예
   ```s
      FROM ubuntu:latest
   
      RUN echo 안녕하세욬 Shell 형식입니다.  ◀ ③
      RUN ["echo", "안녕하세욧 Exec 형식입니다"]  ◀ ②
      RUN ["/bin/bash","-c","echo 'exec 형식에서 bash사용'"]  ◀ ①
   ```   
   문자열을 지정할 때는 홑따옴표를 사용합니다.

   build를 해서 이미지를 생성합니다.
   ```s
      root@ubuntudesk:/mypractice# docker build -t sample_image ./
   ```    

   history 명령어로 build과정을 출력합니다.
   ```s
      root@ubuntudesk:/mypractice# docker image ls
      REPOSITORY       TAG       IMAGE ID       CREATED         SIZE
      sample_image     latest    1c89da963715   9 seconds ago   77.8MB
      tar_ex_image     1.0       379953565739   3 days ago      0B
      
      root@ubuntudesk:/mypractice# docker history sample_image
      IMAGE          CREATED              CREATED BY                                    SIZE     
      1c89da963715   About a minute ago   RUN /bin/bash -c echo 'exec 형식에서 bash사…'  0B   ◀ ①
      <missing>      2 minutes ago        RUN echo 안녕하세욧 Exec 형식입니다             0B   ◀ ②  
      <missing>      2 minutes ago        RUN /bin/sh -c echo 안녕하세욬 Shell 형식입…    0B   ◀ ③    
      <missing>      7 weeks ago          /bin/sh -c #(nop)  CMD ["/bin/bash"]          0B        
      <missing>      7 weeks ago          /bin/sh -c #(nop) ADD file:63d5ab3ef0aab308c… 77.8MB    
      <missing>      7 weeks ago          /bin/sh -c #(nop)  LABEL org.opencontainers.… 0B        
      <missing>      7 weeks ago          /bin/sh -c #(nop)  LABEL org.opencontainers.… 0B        
      <missing>      7 weeks ago          /bin/sh -c #(nop)  ARG LAUNCHPAD_BUILD_ARCH   0B        
      <missing>      7 weeks ago          /bin/sh -c #(nop)  ARG RELEASE                0B        
      root@ubuntudesk-virtual-machine:/home/ubuntu-desk/mypractice_dockerfile# 
   ```   
   ① : Exec형식이지만 /bin/bash 쉘을 명시적으로 지정   
   ② : Exec형식으로 쉘을 경유하지 않고 직접 실행   
   ③ : Shell형식으로 Dockerfile 작성시 없던 '/bin/sh' 쉘 명령어가 출력   

   → /bin/sh를 경유하여 명령을 실행하고 싶을 땐 Shell형식으로 기술, 그 외의 경우는 Exec형식으로 기술   

   
