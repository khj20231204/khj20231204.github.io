---
layout: single
title: docker 재설치
categories: Docker
tag: []
---

1. # 도커 삭제
   ```s
      sudo apt-get purge -y docker-engine docker docker.io docker-ce docker-ce-cli

      sudo apt-get autoremove -y --purge docker-engine docker docker.io docker-ce

      sudo rm -rf /var/lib/docker /etc/docker

      sudo rm /etc/apparmor.d/docker

      sudo groupdel docker

      sudo rm -rf /var/run/docker.sock
   ```   

1. # 도커 설치 
   2. # 패키지 업데이트
      패키지 관리자를 업데이트합니다.   
      ```s
         sudo apt-get update
      ```

   2. # 필요한 패키지 설치
      도커를 설치하기 위해 필요한 패키지들을 설치합니다.   
      ```s
         sudo apt-get install apt-transport-https ca-certificates curl software-properties-common   
      ```

   2. # 도커 GPG 키 추가
      도커의 공식 GPG 키를 추가합니다.   
      ```s
         curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg   
      ```

   1. # 도커 저장소 추가
      도커의 apt 저장소를 추가합니다.   
      ```s
         echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
      ```

   1. # 패키지 업데이트
      패키지 관리자를 업데이트합니다.   
      ```s
         sudo apt-get update
      ```

   1. # 도커 설치
      도커를 설치합니다.   
      ```s
         sudo apt-get install docker-ce docker-ce-cli containerd.io   
      ```   

   1. # 도커 서비스 시작
      도커 서비스를 시작합니다.   
      ```s
         sudo systemctl start docker
      ```   

   1. # 도커 상태 확인
      도커 상태를 확인하여 정상적으로 설치되었는지 확인합니다.   
      ```s
         sudo systemctl status docker
      ```   
      
   이제 도커가 정상적으로 설치되었는지 확인할 수 있습니다.   
