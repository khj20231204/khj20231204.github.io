---
layout: single
title: 리파지토리
categories: Ubuntu
tag: [사용자, 호스트]
---

1. # Repository
   리파지토리는 리눅스 시스템에 설치된 소프트웨어 패키지를 저장하고 유지하는 공간입니다. 리파지토리는 패키지 관리자를 통해 소프트웨어를 설치, 업데이트, 제거할 수 있도록 합니다.
   → 패키지 파일을 모아 배포하는 사이트를 리포지터리.   

1. # 파일 위치 - 레드햇   
   2. 기본적인 패키지 저장소 위치   
   ```s
      /etc/yum.repos.d 

      [root@localhost yum.repos.d]# ls
      backup  docker-ce.repo  google-chrome.repo  this.repo
   ```
   패키지는 일반적으로 /etc/yum.repos.d/ 디렉토리에 위치해 있으며 repo확장자를 가진 파일에 저장됩니다.   
   
   2. 미러사이트 저장 파일 위치 - CentOS8   
   ```s
      /etc/yum.repose.d/this.repo

      [root@localhost yum.repos.d]# cat this.repo
      [BaseOS]
      name=CentOS-$releasever - Base
      baseurl=https://archive.kernel.org/centos-vault/8.0.1905/BaseOS/x86_64/os/
      	  http://linuxsoft.cern.ch/centos-vault/8.0.1905/BaseOS/x86_64/os/
      gpgcheck=0

      [AppStream]
      name=CentOS-$releasever - AppStream
      baseurl=https://archive.kernel.org/centos-vault/8.0.1905/AppStream/x86_64/os/
      	  http://linuxsoft.cern.ch/centos-vault/8.0.1905/AppStream/x86_64/os/
      gpgcheck=0
      ...
   ```
   CentOS8의 경우 this.repo라는 이름의 파일이 있습니다. 이 파일은 레드햇의 공식 저장소와 미러 사이트의 URL, 저장소의 이름, GPG 키 등을 포함합니다. 디렉토리에는 .repo 확장자를 가진 파일들이 있으며, 각 파일은 특정 소프트웨어(패키지) 소스의 정보를 포함하고 있습니다.   

1. # 파일 위치 - 데이반   
   2. 기본적인 패키지 저장소 위치
   ```s
      /var/lib/apt/lists/
   ```
   Ubuntu 패키지는 기본적으로 이 디렉토리에 저장됩니다.

   다른 리눅스 배포판에는 해당 배포판의 패키지 관리자에 따라 리파지토리가 다를 수 있습니다.   

   2. 미러사이트 저장 파일 위치 - ubuntu
   ```s
      /etc/apt/sources.list

      root@ubuntudesk-virtual-machine:/etc/apt# ls -al
      drwxr-xr-x   8 root root  4096 11월 22 23:04 .
      drwxr-xr-x 133 root root 12288 11월 28 17:47 ..
      -rw-rw-r--   1 root root  2825 11월 22 23:06 sources.list
      -rw-r--r--   1 root root  2760 11월 22 23:00 trusted.gpg
      drwxr-xr-x   2 root root  4096 11월 23 09:56 keyrings
      drwxr-xr-x   2 root root  4096 11월 22 16:57 apt.conf.d
      drwxr-xr-x   2 root root  4096  4월  8  2022 auth.conf.d
      drwxr-xr-x   2 root root  4096 11월 22 23:04 trusted.gpg.d
      drwxr-xr-x   2 root root  4096 11월 22 16:56 preferences.d
      drwxr-xr-x   2 root root  4096 11월 23 09:59 sources.list.d

      root@ubuntudesk:/etc/apt# cat sources.list
      # deb cdrom:[Ubuntu 22.04.1 LTS _Jammy Jellyfish_ - Release amd64 (20220809.1)]/ jammy main restricted

      # See http://help.ubuntu.com/community/UpgradeNotes for how to upgrade to
      # newer versions of the distribution.
      deb http://kr.archive.ubuntu.com/ubuntu/ jammy main restricted
      # deb-src http://kr.archive.ubuntu.com/ubuntu/ jammy main restricted
      ...
   ```   
   미러사이트 정보는 sources.list파일에 있습니다. 그리고 추가적인 저장소 설정 파일은 /etc/apt/sources.list.d/ 디렉토리에 위치할 수 있습니다.
   
1. # 리포지터리 구분  

   1)공식 리포지터리(배포판에 처음부터 기본으로 설정된 리포지터리)​   
   해당 리눅스 배포판의 개발자 또는 유지보수팀에 의해 공식적으로 관리되는 소프트웨어 패키지 소스입니다. 이러한 리파지토리에는 배포판에서 지원되는 주요 소프트웨어 패키지가 포함되어 있습니다. 예를 들어, Ubuntu의 공식 리파지토리에는 Ubuntu 개발팀이 유지하는 소프트웨어 패키지가 있습니다.   

   2)서드파티 리포지터리(서드파티에서 제공하는 리포지터리)   
   서드파티 리파지토리는 배포판의 공식 리파지토리 외부에 있는 소프트웨어 패키지 소스입니다. 이러한 리파지토리는 개인, 기업 또는 커뮤니티에 의해 관리되며, 추가적인 소프트웨어 패키지를 제공합니다. 예를 들어, Docker, Chrome 브라우저, VirtualBox 등의 소프트웨어 패키지는 공식 리파지토리가 아닌 서드파티 리파지토리에서 제공될 수 있습니다.   

   3)개인용 리포지터리   
   개인용 리파지토리는 개인이나 조직이 소프트웨어 패키지를 호스팅하고 배포하기 위해 사용하는 리파지토리입니다. 이러한 리파지토리는 공개적으로 액세스할 수 있는 공식 리파지토리 또는 서드파티 리파지토리와는 달리 제한된 사용자 집합에게만 액세스 권한을 부여합니다.   
   ​
*서드파티 : 제3자란 뜻으로  제조자와 사용자 이외 외부의 생산자를 가리키는 뜻
*패키지간 의존성 : 패키지를 설치하기 위해 기존에 설치되어 있어야 하는 패키지와의 관계
