---
layout: single
title: 파티션
categories: Ubuntu
tag: [파티션]
---

1. # 파티션 정보 
   /proc/partitions에서 확인  

1. # 파티션 순서
   주파티션 -> 확장파티션 -> 논리파티션, 스왑파티션   
   2. 주 파티션(Primary Partion)
      부팅이 가능한 파티션   
      하나의 하드디스크에 최대 4개의 주 파티션 분할 가능   
      4개의 파티션 중 하나를 확장파티션으로 지정 후 확장파티션에서 논리파티션을 생성    
   2. 확장 파티션(Extened Partition)
      주파티션 내에 생성   
      하나의 물리적 디스크에 1개만 생성   
   2. 논리 파티션(Logical Partion)
      확장 파티션 안에 생성   
      12개까지 생성 가능   
   2. 스왑 파티션(Swap Partion)
      하드디스크의 일부를 메모리처럼 사용   
      주 파티션 또는 논리 파티션에 생성   
      프로그램 실행시 부족한 메모리 용량을 하드디스크가 대신함   
      리눅스 설치 시 반드시 설치되어야 하는 영역     
      크기는 보통 메모리에 2배로 권장   

1. # 디바이스 명 
   2. 하드디스크 유형
      hd: IDE 또는 ATA 방식 디스크   
      sd: SCSI 또는 USB 방식 디스크   
   2. 파티션 종류 
      1 ~ 4 : 주 파티션 또는 확장 파티션에 설정되는 숫자   
   5번부터 : logical 파티션   
   2. 하드디스크 우선 순위
      한 케이블에 하드 디스크를 2개씩 묶어 master과 slave로 구분   
      첫 번째(Primary) 하드디스크 - master : a   
      첫 번째(Primary) 하드디스크 - slave : b   
      두 번째(Secondary) 하드디스크 - master : c   
      두 번째(Secondary) 하드디스크 - slave : d 
      ... 
      <br>
      (하드디스크 4개일 경우)  
      Primay Master  - hda     
      Primary Slave - hdb   
      Secondary Mater - hdc   
      Secondary Slave - hdd   
      <br>

1. # 명칭
      hda1 ~ hda3 : primay master에서 주 파티션   
      hda4 : primay master에서 확장 파티션   
      hda5 ~ hda16 : primay master에서 논리 파티션   
      <br>
      hdb1 ~ hdb3 : primay slave에서 주 파티션   
      hdb4 : primay slave에서 확장 파티션   
      hdb5 ~ hdb16 : primay slave에서 논리 파티션   
      ...   

      <br>
      (ex)   
      hda3 : IDE방식의 디스크/primay master/3번째 주파티션    
      hdd5 : IDE방식의 디스크/secondary slave/첫번째 논리파티션  
      <br> 
      <span style="color">a,b,c,..는 하드디스크</span>
      <br>
      <span style="color">숫자는 파티션</span>
