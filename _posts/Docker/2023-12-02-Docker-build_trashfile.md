---
layout: single
title: dockerignore
categories: Docker
tag: []
---

빌드를 하면 빌드를 실행한 디렉토리 아래에 있는 모든 파일이 Docker 데몬으로 전송 됩니다. 그렇기 때문에 빌드에서 제외하고 싶은 파일이 있는 경우 '.dockerignore' 이라는 이름의 파일 안에 제외하고 싶은 파일명을 적으면 됩니다.

예)dummyfile 제외하기
```s
  FROM ubuntu

  ADD dummyfile /tmp/dummyfile
```   

docker build 명령은 Dockerfile을 포함하는 디렉토리와 해당 디렉토리의 서브 디렉토리까지 모두 Docker 데몬으로 전송합니다. 만약 루트 디렉토리에 Dockerfile을 만들고 build를 시키면 모든 파일이 Docker 데몬으로 전송이 됩니다. 그렇기 때문에 빈 디렉토리를 생성 후 Dockerfile을 빈 디렉토리에 가져다 놓은 후 build를 해야 합니다.   

*Docker 데몬은 Docker의 서버 측입니다. 빌드시 dockerfile과 같은 디렉토리에 있는 파일들이 이미지에 추가되지는 않습니다.