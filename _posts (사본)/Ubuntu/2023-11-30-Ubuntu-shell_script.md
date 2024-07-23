---
layout: single
title: 쉘 스크립트
categories: Ubuntu
tag: []
---

1. # docker삭제 쉘 스크립트
   ```s
   #!/bin/bash
   echo $'Start ----- Docker Delete -----'

   sudo apt-get purge -y docker-engine docker docker.io docker-ce docker-ce-cli   

   sudo apt-get autoremove -y --purge docker-engine docker docker.io docker-ce   

   sudo rm -rf /var/lib/docker /etc/docker   

   sudo rm /etc/apparmor.d/docker   

   sudo groupdel docker   

   sudo rm -rf /var/run/docker.sock   
   ```
1. # docker설치 쉘 스크립트
   ```s
   #!/bin/sh
   
   sudo apt-get update   

   sudo apt-get install apt-transport-https ca-certificates curl software-properties-common   

   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg   

   echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null   

   sudo apt-get update   

   sudo apt-get install docker-ce docker-ce-cli containerd.io   

   sudo docker info
   ```   

1. # 실행 방법
   리눅스에서 source는 스크립트 파일을 현재 셸 세션에서 실행하는 명령어입니다. source 명령어는 주로 환경 변수, 함수 또는 별칭을 포함하는 스크립트 파일을 로드할 때 사용됩니다.   

   source 명령어는 스크립트 파일을 현재 셸 세션 내에서 실행하므로, 스크립트 파일이 새로운 서브 셸을 생성하지 않고 현재 셸 환경에 변경사항을 적용할 수 있습니다. 이는 스크립트 파일에서 정의된 환경 변수, 함수 또는 별칭을 현재 셸 세션에서 사용할 수 있게 해줍니다.   

   또한, source 명령어는 .(점) 명령어로도 사용할 수 있습니다. .(점) 명령어는 source 명령어의 별칭이며 동일한 기능을 수행합니다. 따라서 source script.sh와 . script.sh는 동일한 역할을 합니다.   

   ```
      root@ubuntudesk:/home# source docker_del.sh
      root@ubuntudesk:/home# . docker_del.sh
   ```
