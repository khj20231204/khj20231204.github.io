---
layout: single
title: 명령어(네트워크,시스템종료)
categories: Ubuntu
tag: [traceroute, nslookup, dig, host, hostname, shutdown, reboot, init, halt]
---

1. ## 네트워크
   2. ### traceroute
      목적지 호스트까지의 경로를 표시하고 그 구간의 정보를 기록하는 명령어   
      목적지 호스트까지 패킷 전송 지역을 측정   
      목적지 호스트로 향하는 경로상에 어떤 장애가 있는 경우 위치를 파악   
      tracerout [도메인명 혹은 IP주소]   

   2. ### nslookup
      도메인명으로 IP주소를 조회하거나, IP주소로 도메인명을 조회하는 명령어   
      nslookup [옵션] [호스트명]   

   2. ### dig
      nslookup과 비슷한 기능을 가진 명령어로, 호스트명에 대한 IP주소 정보를 조회하거나, IP주소에 대한 호스트명을 조회하는 명령어   
      서버명은 확인하고자 할 네임 서버를 지정하는 것이며 지정하지 않을 경우 /etc/resolv에 등록된 네임 서버를 이용하여 루트 서버를 조회   

   2. ### host
      호스트명을 알고 있는데 IP주소를 모르거나 그 반대인 경우 사용하는 명령어   
      호스트명을 이용하면 IP주소 뿐만아니라 하위 호스트명도 조회할 수 있습니다.   
      호스트는 시스템에 등록된 DNS서버를 이용   

   2. ### hostname
      시스템 이름을 확인하거나 변경할 때 사용하는 명령어   

1. ## 시스템 종료 
   2. ### shutdown
      시스템을 종료하거나 재부팅하는 명령어   

   2. ### init
      shutdown과 동일한 기능을 가진 명령어   

   2. ### reboot 
      시스템을 재부팅하는 명령어   
      
   2. ### halt
      시스템을 종료하는 명령어   

  

  
      
   