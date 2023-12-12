---
layout: single
title: 컨테이너 네트워크
categories: Docker
tag: []
---

1. # 네트워크 작성
   ```s
      docker network create [옵션] 네트워크명
   ```   

   |  옵션  |  설명  |
   |:------:|:------:|
   |--driver, -d|네트워크 브리시 또는 오버레이(기본값은 bridge)|
   |--ip-range|컨테이너에 할당하는 IP 주소의 범위를 지정|
   |--subnet|서브넷을 CIDR 형식으로 지정|
   |--ipv6|IPv6 네트워크를 유효화할지 말지(true/false)|
   |-label|네트워크에 설정하는 라벨|
   
   *오버레이 : 여러개의 호스트에 걸쳐있는 네트워크   

   bridge로 'web-network'라는 네트워크를 생성   
   ```s
      docker network create drive=bridge web-network
   ```   

1. # 오버레이 네트워크
   오버레이 네트워크는 가상의 네트워크를 생성하여 도커 컨테이너들이 서로 통신할 수 있도록 하는 기술입니다. 오버레이 네트워크는 여러 호스트에 걸쳐 있는 컨테이너들을 연결하기 위해 사용됩니다.   

   오버레이 네트워크는 도커 서비스 디스커버리와 로드 밸런싱을 위해 사용되기도 합니다. 여러 호스트에 걸쳐 있는 컨테이너들은 오버레이 네트워크를 통해 서로 통신할 수 있으며, 호스트 간의 통신은 가상의 네트워크를 통해 이루어집니다.   

   오버레이 네트워크는 도커 스웜 모드와 함께 자주 사용됩니다. 도커 스웜은 여러 호스트를 클러스터로 구성하여 컨테이너들을 분산 관리하는 기술인데, 오버레이 네트워크는 이러한 클러스터 환경에서 컨테이너들을 연결하는 데 사용됩니다.   

   오버레이 네트워크는 가상 네트워크를 생성하고, 각 컨테이너에 가상 IP 주소를 할당하여 통신하게 됩니다. 이를 통해 컨테이너들은 물리적인 호스트 간의 제약 없이 자유롭게 통신할 수 있습니다.   

1. # 네트워크 연결

   1)연결 - connect   
   Docker 컨테이너를 Docker 네트워크에 연결 합니다. 연결 후에는 동일한 네트워크상에 있는 다른 컨테이너와도 통신을 할 수 있습니다. 컨테이너 연결은 IP주소 뿐만 아니라 컨테이너명 또는 컨테이너ID를 이용할 수 있습니다.   
   ```s
      docker network connect [옵션] 네트워크명 컨테이너명
   ```   

   |옵션|설명|
   |:-----:|:-----:|
   |--ip|IPv4 주소|
   |--ip6|IPv6 주소|
   |--alias|앨리어스명|
   |--link|다른 컨테이너에 대한 링크|

   web-network란 네트워크에 webfront란 컨테이너를 연결   
   ```s
      docker network connect web-network webfront
   ```   

   web-network란 네트워크를 run명령시 연결   
   ```s
      docker container run -itd --name=webap --net=web-network nginx
   ```   
   -id : 결과를 콘솔에 출력   
   -d : 백그라운드 실행   
   --name : 컨테이너 이름을 webap로 설정
   --net : web-network란 네트워크 연결(연결 전 생성되어 있어야 함)   
   nginx : nginx이미지를 가져옴   

   2)연결해제 - disconnect   
   ```s
      docker network disconnect web-network webfront
   ```   
   web-network란 네트워크와 webfront란 컨테이너 연결 해제   

1. # 네트워크 목록 표시
   ```s
      docker network ls [옵션]
   ```   

   |  옵션  |  설명  |
   |:------:|:------:|
   |--filter=[], -f|출력을 필터링|
   |--no-trunc|상세 정보를 출력|
   |--quiet, -q|네트워크 ID만 표시|

   |filter 목록|
   |:--------:|
   |driver|
   |id|
   |label|
   |name|
   |scope|
   |type|

   Docker는 기본값으로 bridege, host, none 이 세 개의 네트워크를 만듭니다.   

   1)Bridge (기본값): 도커가 설치된 호스트 머신에 가상의 브리지 네트워크를 생성하여 컨테이너들이 이 네트워크에 연결됩니다. 컨테이너들끼리는 브리지 네트워크를 통해 통신할 수 있으며, 호스트 머신과도 통신할 수 있습니다. 브리지 네트워크를 사용하는 컨테이너는 동일한 네트워크 내에서 IP 주소를 할당받습니다.   

   2)Host: 호스트 모드를 사용하면, 컨테이너는 호스트 머신의 네트워크 스택을 공유합니다. 즉, 컨테이너는 호스트 머신과 동일한 IP 주소를 가지며, 호스트 머신과 동일한 네트워크 인터페이스를 사용하게 됩니다. 따라서 컨테이너는 호스트 머신과 완전히 동일한 네트워크 환경을 가지게 됩니다.   

   3)None: 네트워크 모드를 None으로 설정하면, 컨테이너는 네트워크를 사용할 수 없습니다. 컨테이너는 완전히 격리되어 있으며, 다른 컨테이너나 호스트와 통신할 수 없습니다. 이 모드는 네트워크를 필요로하지 않는 애플리케이션 컨테이너나 테스트 목적으로 사용될 수 있습니다.   

   bridge네트워크만 검색   
   ```
      docker network ls --filter driver=bridge
   ```   

1. # 네트워크 상세 정보 확인
   ```
      docker network inspect [옵션] 네트워크명
   ```   

   예)연습용으로 만든 ex_network 상세정보   
   ```s
      root@ubuntudesk-virtual-machine:/home/ubuntu-desk# docker network inspect ex_network
      [
          {
              "Name": "ex_network",
              "Id": "2e4e9dcd76a1fad1bfdd605d68b5e0769fddbdc004e97804533182eb95b9d61e",
              "Created": "2023-11-26T17:17:46.560508058+09:00",
              "Scope": "local",
              "Driver": "bridge",    ☜bridge방식
              "EnableIPv6": false,
              "IPAM": {
                  "Driver": "default",
                  "Options": {},
                  "Config": [
                      {
                          "Subnet": "172.18.0.0/16",  ☜서브넷
                          "Gateway": "172.18.0.1"  ☜게이트웨이
                      }
                  ]
              },
              "Internal": false,
              "Attachable": false,
              "Ingress": false,
              "ConfigFrom": {
                  "Network": ""
              },
              "ConfigOnly": false,
              "Containers": {     ☜연결된 컨테이너 내용
                  "087580992b394da4dc0caa415c74994f05234196f7e6fe650e28cbaf49d795cb": {
                      "Name": "ex_nginx",    ☜컨테이너명
                      "EndpointID": "3175dc733eb03e269e845dfc3596b4e3005287e8aa0b335fc57457ccb9afe36c",
                      "MacAddress": "02:42:ac:12:00:02",
                      "IPv4Address": "172.18.0.2/16",    ☜IPv4주소
                      "IPv6Address": ""
                  }
              },
              "Options": {},
              "Labels": {}
          }
      ]
   ```   
   
1. # 네트워크 삭제
   ```
      docker network rm 네트워크명
   ```   


