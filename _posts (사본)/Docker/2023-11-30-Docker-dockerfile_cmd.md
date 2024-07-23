---
layout: single
title: dockerfile CMD
categories: Docker
tag: [cmd]
---

1. # CMD명령어
   RUN명령이 이미지를 생성하기 위한 명령어라면 CMD명령어는 이미지를 바탕으로 생성된 컨테이너 안에서 실행하는 명령어입니다. Dockerfile에서는 한개의 CMD명령어를 실행할 수 있는데 만약 여러개 가 지정된다면 가장 마지막에 작성된 명령이 실행됩니다.   
   예를 들어 Nginx 설치는 RUN명령으로 하고, Nginx를 데몬으로 컨테이너 안에서 동작시키는 명령어가 CMD입니다.   

   ```s
      CMD [실행하고 싶은 명령]
   ```   

1. # Shell 형식으로 기술
   ```s
      CMD nginx -g 'daemon off;'
   ```   
   -g : nginx 설정 변경   
   daemon off : nginx를 백그라운드로 실행하지 않고 현재 터미널 세션에서 실행. 디버깅을 할 때 코드 수정이나 설정 변경시 변경사항을 빠르게 확인하기 위해서 사용

1. # Exec 형식으로 기술
   ```s
      CMD ["nginx","-g","daemon off;"]
   ```   
   Exec형식은 쉘을 호출하지 않습니다. 인수는 JSON배열로 지정. daemon off를 해서 백그라운드가 아니라 포어그라운드로 실행   

