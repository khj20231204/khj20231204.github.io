---
layout: single
title: install
categories: CentOS
tag: [yum, rpm, systemctl, wget]
---

1. # rpm
   Red Hat Package Manager의 약자로, 리눅스에서 소프트웨어 패키지를 설치, 업데이트, 제거하는 도구입니다. rpm은 패키지의 이름, 버전, 설치 경로, 의존성 등의 정보를 포함하고 있으며, 명령줄에서 rpm 명령어를 사용하여 패키지를 관리할 수 있습니다. rpm은 개별 패키지를 다운로드하여 설치할 수 있으며, 로컬 파일 시스템에서 패키지를 찾을 수도 있습니다.   
   그러나 의존성 문제를 직접 해결해야 하고 필요한 의존성 패키지를 수동으로 설치해야 합니다. 따라서 rpm은 CentOS에서 개별 패키지 관리에 사용되는 도구입니다.   

1. # yum
   Yellowdog Updater Modified의 약자로, 리눅스 시스템에서 패키지를 자동으로 설치, 업데이트, 제거하는 패키지 관리 도구입니다. yum은 rpm을 기반으로 하며, 패키지 관리를 편리하게 처리할 수 있도록 다양한 기능을 제공합니다. yum을 사용하면 의존성 문제를 자동으로 처리하고 필요한 의존성 패키지를 자동으로 설치할 수 있습니다.   
   또한, 패키지 저장소에서 패키지를 다운로드하여 설치할 수 있으며, 패키지의 업데이트나 제거도 간편하게 할 수 있습니다. 따라서 yum은 CentOS에서 편리하고 사용하기 쉬운 패키지 관리 도구입니다.   

   - yum 명령어
   yum install [패키지명]: 패키지를 설치합니다.   
   yum remove [패키지명]: 패키지를 제거합니다.   
   yum update [패키지명]: 패키지를 업데이트합니다.   
   yum upgrade: 모든 패키지를 최신 버전으로 업그레이드합니다.   
   yum search [키워드]: 패키지를 검색합니다.   
   yum info [패키지명]: 패키지에 대한 정보를 확인합니다.   
   yum list: 시스템에 설치된 모든 패키지를 나열합니다.   
   yum clean [옵션]: 캐시된 RPM 패키지를 정리합니다.   
   yum repolist: 사용 가능한 레파지토리 목록을 표시합니다.   
   yum check-update: 사용 가능한 패키지의 업데이트를 확인합니다.   
   yum groupinstall [그룹명]: 패키지 그룹을 설치합니다.   
   yum groupremove [그룹명]: 패키지 그룹을 제거합니다.   
   yum provides [파일명]: 파일이 어느 패키지에 속하는지 확인합니다.   

   *특정 파일 이름 포함 검색   
   ```
      yum info "*aa*"
   ```   
   aa를 포함하는 파일 검색   

1. # yum-utils
   yum-utils는 다양한 유틸리티 도구를 제공하여 yum 패키지 관리자의 기능을 보완하고 확장합니다.  yum-utils 패키지를 설치하면 다음과 같은 유틸리티 도구를 사용할 수 있습니다:

   yum-builddep: 패키지를 빌드하기 위해 필요한 의존성 패키지를 설치합니다.   
   yum-config-manager: Yum 저장소 관리자로, 저장소 설정을 관리하고 구성할 수 있습니다.   
   yum-debug-dump 및 yum-debug-restore: 디버그 정보를 저장하고 복원하는 데 사용됩니다.   
   yumdownloader: 패키지를 다운로드합니다.   
   package-cleanup: 시스템에서 사용하지 않는 패키지 및 캐시를 정리합니다.   
   verifytree: 패키지에 대한 트리 구조를 확인합니다.   
   repo-rss: Yum 저장소에 대한 RSS 피드를 생성합니다.   
   repo-graph: Yum 저장소에 대한 그래프를 생성합니다.   
   repoquery: 저장소에서 패키지 정보를 쿼리합니다.   
   yumdb: Yum 데이터베이스를 쿼리하고 관리합니다.   
   
   위 목록은 yum-utils 패키지에서 제공되는 일부 도구입니다. 이 외에도 다른 유용한 도구들이 포함되어 있을 수 있습니다. yum-utils 패키지를 설치한 후에는 yum <도구이름> 형식으로 각 도구를 실행할 수 있습니다.   

   - 설치
   ```
      yum install -y yum-utils
   ```   
   명령어를 실행하면 yum 패키지 관리자는 미리 설정된 저장소에서 yum-utils 패키지를 다운로드하여 설치합니다. 기본적으로 CentOS, Fedora 등의 리눅스 배포판에서는 CentOS 저장소 또는 Fedora 저장소를 사용하여 패키지를 다운로드합니다. 따라서 인터넷에 연결된 상태에서 해당 저장소에서 yum-utils 패키지를 다운로드하여 설치합니다.   

1. # yum-config-manger
   yum-config-manager은 리눅스에서 사용되는 yum 패키지 관리자의 구성을 관리하는 명령어입니다. 이 명령어를 사용하여 저장소를 추가, 제거, 활성화, 비활성화 등 다양한 작업을 수행할 수 있습니다.   
 
1. # 저장소
   CentOS의 기본 저장소 주소는 http://mirror.centos.org/centos/버전번호/os/아키텍처/ 입니다. 여기서 버전번호는 사용하는 CentOS 버전에 따라 다르며, 아키텍처는 시스템의 아키텍처에 따라 x86_64 또는 i386 등이 될 수 있습니다. 예를 들어, CentOS 7의 기본 저장소 주소는 http://mirror.centos.org/centos/7/os/x86_64/ 입니다.   
   
   CentOS 기본 저장소에 있는 유틸 목록은 다음과 같은 명령어를 통해 확인할 수 있습니다:   
   ```
      yum list available
   ```   
   위 명령어를 실행하면 CentOS 기본 저장소에 있는 모든 패키지 목록을 확인할 수 있습니다. 이 중에서 원하는 유틸리티를 찾아서 설치할 수 있습니다.   

1. # systemctl
   systemctl은 리눅스 시스템에서 서비스의 상태를 관리하는 명령어입니다. systemctl을 사용하여 서비스의 시작, 중지, 재시작, 상태 확인 등의 작업을 수행할 수 있습니다. 이 명령어는 대부분의 최신 리눅스 배포판(예: CentOS, Fedora, Ubuntu)에서 사용할 수 있습니다.   

   - 주요 사용법   
   서비스 시작: systemctl start `<서비스명>`   
   서비스 중지: systemctl stop `<서비스명>`   
   서비스 재시작: systemctl restart `<서비스명>`   
   서비스 상태 확인: systemctl status `<서비스명>`   
   부팅 시 자동 시작 설정: systemctl enable `<서비스명>`   
   부팅 시 자동 시작 비활성화: systemctl disable `<서비스명>`   
   예를 들어, Apache 웹 서버를 시작하려면 다음과 같이 입력할 수 있습니다:   
   ```
      sudo systemctl start httpd   
   ```   
   systemctl 명령어를 통해 서비스를 관리하면 시스템의 서비스 상태를 쉽게 확인하고 제어할 수 있습니다.   

 1. # wget
   wget은 리눅스 및 유닉스 시스템에서 파일을 다운로드하는 명령어입니다. wget은 웹 서버에서 파일을 가져와서 로컬 시스템에 저장할 수 있습니다.   

   - 주요 사용법   
   파일 다운로드: wget `<파일 URL>`   
   다운로드 위치 지정: wget -P `<다운로드 경로> <파일 URL>`   
   백그라운드로 다운로드: wget -b `<파일 URL>`   
   재귀적으로 다운로드: wget -r `<웹페이지 URL>`   
   다운로드 제한 속도 설정: wget --limit-rate=`<속도> <파일 URL>`   
   예를 들어, wget을 사용하여 이미지 파일을 다운로드하려면 다음과 같이 입력할 수 있습니다:   
   wget http://example.com/image.jpg   
   wget은 웹에서 파일을 다운로드하는 간단하고 편리한 방법을 제공합니다. 다운로드한 파일을 사용하거나 웹 사이트의 콘텐츠를 백업하는 데 유용하게 사용할 수 있습니다.   

1. # yum과 wget
   wget과 yum은 모두 리눅스 시스템에서 사용되는 명령어이지만, 다른 목적과 용도를 가지고 있습니다.   
   
   __wget:__   
   wget은 주로 파일을 웹 서버에서 다운로드하는 데 사용됩니다. 주어진 URL에서 파일을 직접 다운로드하고 로컬 시스템에 저장합니다. 다운로드한 파일을 로컬 시스템에 저장하는 것이 주된 목적이며, 다른 의존성 패키지를 자동으로 설치하는 기능은 제공하지 않습니다. 예를 들어, wget http://example.com/file.zip은 example.com에서 file.zip을 다운로드하여 현재 작업 디렉토리에 저장합니다.   
      
   __yum:__   
   yum은 리눅스 시스템에서 패키지 관리를 위해 사용되는 명령어입니다. 패키지 관리자로서, 의존성을 자동으로 해결하고 필요한 패키지를 설치, 업데이트, 제거하는 데 사용됩니다. 저장소(repositories)에서 패키지를 찾아 설치하므로, 인터넷에 연결된 상태에서 사용됩니다. 예를 들어, yum install package-name은 패키지 관리자를 통해 package-name 패키지를 설치하고 필요한 의존성 패키지도 함께 설치합니다. 따라서, wget은 파일을 다운로드하는 데 사용되고, yum은 패키지 관리를 위한 명령어입니다. 각각의 목적과 용도에 따라 적절한 상황에서 사용됩니다.   

1. # CentOS와 Ubuntu

   | CentOS  | Ubuntu | 기능 |
   |:-------:|:------:|:-------:|
   |   yum   |   apt  | 패키지 관리<br>yum은 rpm을 기반, apt는 dpkg를 기반<br>의존성 문제 자동 해결 |
   |   rpm   |  dpkg  | 패키지 관리<br>의존성 문제 직접 해결 |
   |   wget  |  curl  | HTTP, HTTPS, FTP 프로토콜을 사용하여 파일을 다운로드<br>→인터넷 주소로 다운로드 |
   
   *wget과 curl은 CentOS, Ubuntu 구별없이 사용 함
     
   
   