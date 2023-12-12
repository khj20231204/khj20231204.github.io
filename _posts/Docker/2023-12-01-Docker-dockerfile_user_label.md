---
layout: single
title: dockerfile USER와 LABEL
categories: Docker
tag: []
---

1. # USER 명령어
   사용자를 지정하기 위한 명령어입니다.
   ```s
      USER [사용자명/UID]
   ```   

   예)
   ```s
      USER superman

      RUN whoami
      RUN echo "사용자 지정"
   ```   

1. # LABEL 명령어
   이미지에 버전 정보아 작성자 정보, 코멘트 등과 같은 정보를 제공하는 명령어입니다.   

   ```s
      LABEL 키=값
   ```   

   예)
   ```
      LABEL title="WebAPI"
      LABEL version=1.0.0
      LABEL discription="This image is WebApplicationAPI"
   ```   
   