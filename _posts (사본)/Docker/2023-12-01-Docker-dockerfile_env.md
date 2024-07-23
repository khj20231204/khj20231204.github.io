---
layout: single
title: dockerfile 환경 설정
categories: Docker
tag: []
---

1. # 환경변수 설정
   환경변수를 설정하는 방법은 다음 2가지입니다.

   ```s
      ENV [key] [value]

      ENV [key] = [value]
   ```   

1. # key value 형식으로 지정
   단일 환경변수에 하나의 값을 설정합니다. 첫 번째 공백 앞을 key로 설정하면 그 이후는 모두 문자열로서 취급합니다. 공백이나 따옴표도 전부 문자열로 취급   

   | 키 명 |  값  |
   |:-----:|:------:|
   | key1 | value1 value2 |
   | key2 | "value1 value2"|
   | key3 | value1 | 

   ```s
      ENV key1 = value1 value2
      ENV key1 = "value1 value2"
      ENV key1 = value1
   ```   
   ENV 명령이 3줄에 걸쳐 있으므로 3개의 도커 이미지를 겹쳐서 만들어집니다.

1. # key=value 형식으로 지정
   ```s
      ENV key1=value1 value2 \
          key2="value1 vluae2" \
          key3=value1
   ```
   한 번에 여러 개의 값을 설정할 때 이용합니다. 여기서는 하나의 ENV 명령으로 여러 개의 값을 설정하므로 만들어지는 Docker이미지는 한 개입니다. 변수 앞에 \를 추가하면 이스케이프 처리를 할 수 있습니다.

   ENV 명령으로 지정한 환경변수는 컨테이너 실행 시의 docker container run 명령의 --env옵션을 사용하면 변경 가능   

