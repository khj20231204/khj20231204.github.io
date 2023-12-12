---
layout: single
title: dockerfile ONBUILD
categories: Docker
tag: [cmd]
---

1. # ONBUILD
   빌드 후 실행할 명령을 이미지 안에 설정하기 위한 명령입니다. 예를 들어 Dockerfile에 ONBUILD명령을 사용하여 어떤 명령을 실행하도록 설정하여 빌드하고 이미지를 작성합니다. 이 이미지를 다른 Dockerfile에서 베이스 이미지로 설정하여 빌드했을 때  ONBUILD 명령에서 지정한 명령을 실행시킬 수 있습니다.   

   step 1. 부모 dockerfile 생성   
   ```s
      FROM ubuntu

      ONBUILD RUN echo "hello"
   ```   

   step 2. 부모 dockerfile 빌드   
   ```s
      root@ubuntudesk:/mydir2# docker build -t hello_image ./   "hello_image 생성"
   ```   

   step 3. 자식 dockerfile에서 부모 이미지 호출   
   ```s
      FROM hello_image
   ```   

   step 4. 자식 dockerfile을 빌드   
   ```s
      root@ubuntudesk:/mydir3# docker build -t second_hello_image ./
   ```   

   step 5. 자식 이미지 run   
   ```s   
      root@ubuntudesk:/mydir3# docker container run -it second_hello_image 
      root@358e3b18b35b:/# ls
   ```   

1. # ONBUILD 사용 목적
   웹 시스템을 구출할 때 OS 설치 및 환경 설정이나 웹 서버 설치 및 각종 플러그인 설치 등과 같은 인프라 환경 구축과 관련된 부분을 베이스 이미지로 작성합니다. 이때 ONBUILD명령으로 이미지 안에 개발한 프로그램을 전개하는 명령(ADD나 COPY명령)을 지정합니다. 애플리케이션 개발자는 애플리케이션의 구축 부분을 코딩하고 이미 작성이 끝나 베이스 이미지를 바탕으로 한 이미지를 작성합니다. 이 이미지 안에는 프로그래밍이 끝난 업무 애플리케이션이 전개됩니다.   

1. # CMD와 ONBUILD의 차이점
   ONBUILD는 부모 이미지에서 빌드된 이미지를 자식 이미지로 사용할 때 특정 명령을 실행하는 데 사용됩니다. 즉, 부모 이미지에서 빌드된 이미지를 기반으로 새로운 이미지를 빌드할 때 ONBUILD 지시문에 지정된 명령이 실행됩니다. 자식 이미지에서 ONBUILD 지시문을 사용하여 특정 작업을 수행하고자 할 때 유용합니다.   

   CMD는 Docker 컨테이너가 시작될 때 실행되는 명령을 지정하는 데 사용됩니다. CMD 지시문은 Dockerfile에서 한 번만 사용할 수 있으며, 마지막에 지정된 CMD 지시문이 유효하게 됩니다. 즉, Docker 컨테이너가 시작될 때 실행할 명령을 정의하는 역할을 합니다.   

   요약하자면, ONBUILD는 부모 이미지에서 자식 이미지를 빌드할 때 특정 작업을 수행하는 데 사용되고, CMD는 Docker 컨테이너가 시작될 때 실행할 명령을 지정하는 데 사용됩니다.   