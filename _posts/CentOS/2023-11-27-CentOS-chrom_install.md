---
layout: single
title: 크롬 설치
categories: CentOS
tag: 
---


```
   [root@localhost ~]# wget https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm

   [root@localhost ~]# sudo yum localinstall -y google-chrome-stable_current_x86_64.rpm

   sudo rpm -ivh google-chrome-stable_current_x86_64.rpm
```

error
```
   [root@localhost ~]# sudo yum localinstall -y google-chrome-stable_current_x86_64.rpm
   마지막 메타 데이터 만료 확인 : 22:09:39 전에 2023년 11월 21일 (화) 오후 05시 09분 18초.
   종속성이 해결되었습니다.
   ================================================================================
    꾸러미                    아키텍처  버전                 리포지토리       크기
   ================================================================================
   Installing:
    google-chrome-stable      x86_64    119.0.6045.159-1     @commandline     46 M
   종속성 설치:
    mesa-vulkan-drivers       x86_64    18.3.1-5.el8_0       AppStream       2.2 M
    vulkan-loader             x86_64    1.1.82.0-1.el8       AppStream       107 k
    liberation-fonts          noarch    1:2.00.3-4.el8       BaseOS           19 k
    liberation-serif-fonts    noarch    1:2.00.3-4.el8       BaseOS          607 k

   거래 요약
   ================================================================================
   설치  5 꾸러미

   총합 크기: 48 M
   설치 크기 : 327 M
   패키지 다운로드중:
   [SKIPPED] mesa-vulkan-drivers-18.3.1-5.el8_0.x86_64.rpm: Already downloaded    
   [SKIPPED] vulkan-loader-1.1.82.0-1.el8.x86_64.rpm: Already downloaded          
   [SKIPPED] liberation-fonts-2.00.3-4.el8.noarch.rpm: Already downloaded         
   [SKIPPED] liberation-serif-fonts-2.00.3-4.el8.noarch.rpm: Already downloaded   
   --------------------------------------------------------------------------------
   합계                                            291 MB/s | 2.9 MB     00:00     
   트랜잭션 점검 실행 중
   트랜잭션 검사가 성공했습니다.
   트랜잭션 테스트 실행 중
   다운로드 된 패키지는 다음 번 성공적인 트랜잭션까지 캐시에 저장되었습니다.
   캐시 된 패키지를 제거하려면 'dnf clean packages'.
   오류: 거래 확인 오류 :
     package google-chrome-stable-119.0.6045.159-1.x86_64 does not verify: Payload SHA256 digest: BAD (Expected 00b01bbd5ffa7f2a1032ab1d72bca46e42f3704cf56e863befabb88acf6d9ade != 4a2e9b18d08b4ad263137cccd10793534e381a999deb5a1605646519f695c22d)

   오류 요약
```