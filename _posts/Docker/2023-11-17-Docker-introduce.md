---
layout: single
title: 도커란?
categories: Docker
tag: []
---

1. # 도커란?
   컨테이너 기술을 사용하여 애플리케이션의 실행 환경을 구축 및 운용하기 위한 플랫폼입니다. 애플리케이션의 실행에 필요한 것을 모아 Docker 이미지로 관리함으로써 애플리케이션의 이식성을 높일 수 있습니다.   
   서버를 부팅할 때 실행되는 운영체제를 일반적으로 호스트OS라고 부르며, 도커 컨테이너는 호스트OS 위에서 실행되는 격리된 공간입니다. 컨테이터 자체에 특별한 권한을 주지 않는 한 컨터이너 내부에서 수많은 소프트웨어를 설치하고 설정 파일을 수정해도 호스트OS에는 영향을 주지 않습니다. 즉 독립된 개발 환경을 보장 받을 수 있습니다.    
   컨터이너 내부에서 작업한 파일을 운영 환경에 배포하려고 한다면, 해당 컨테이너를 '도커 이미지'라고 하는 패키지로 만들어 운영 서버에 전달만 하면 됩니다. 서버를 개발할 때 사용했던 환경을 다른 서버에서도 컨테이너로서 똑같이 복제할 수 있기 때문에 개발/운영 환경의 통합이 가능해집니다.   
   게다가 도커 이미지는 가상 머신의 이미지와 달리 커널을 포함하고 있지 않기 때문에 이미지 크기가 그다지 크지 않습니다. 또한 도커는 이미지 내용을 레이어 단위로 구성하며, 중복되는 레이어를 재 사용할 수 있어서 배포 속도가 매우 빨라진다는 장점이 있습니다.   

1. # 모놀리스와 마이크로 서비스
   2. 모놀리스 구소 : 소프트웨어의 여러 모듈이 상호 작용하는 로직을 하나의 프로그램 내에서 구동시키는 방식   
   2. 마이크로 서비스 : 여러 모듈을 독립된 형태로 구성하기 때문에 언어에 종속되지 않고 변화에 빠르게 대응할 수 있으며, 각 모듈의 관리가 쉬워집니다.   

1. # Container란?
   호스트 OS상에 논리적인 구획입니다. 이 구획 안에서 애플리케이션을 작동시키기 위해 필요한 라이브러리나 애플리케이션 등을 하나로 모아, 마치 별도의 서버인 것처럼 사용할 수 있게 만든 것입니다.   
   물리 서버상에 설치한 호스트 OS(자신의 컴퓨터에 실제 설치한 OS)의 경우 하나의 OS 상에서 움직이는 여러 애플리케이션은 똑같은 시스템 리소스를 사용합니다. 이때 작동하는 여러 애플리케이션은 디렉토리를 공유하고, 동일한 IP주소로 통신합니다. 따라서 여러 애플리케이션에서 사용하고 있는 미들웨어나 라이브러리의 버전이 다른 경우에는 각 애플리케이션이 서로 영향을 받지 않도록 주의해야합니다.   
   하지만 컨테이너 기술을 사용하면 OS나 디렉토리, IP 주소 등과 같은 시스템 자원을 마치 각 애플리케이션이 점유하고 있는 것처럼 보이게 할 수 있습니다. 호스트 OS의 리소스를 논리적으로 분리시키기 때문입니다.   

1. # 서버 가상화 기술
   2. 호스트형 서버 가상화    
   하드웨어 상에 기초가 되는 호스트 OS를 설치하고, 호스트 OS에 가상화 소프트웨어를 설치한 후, 이 가상화 소프트웨어 상에서 게스트 OS를 작동시키는 기술입니다. 오라클의 'VM Virtual Box'와 VMware의 'VMare Workstation Player'등이 있습니다. 하지만 이 방식은 컨테이너와 다르게 호스트 OS 상에서 다른 게스트 OS를 움직이고 있기 때문에 호스트 OS상의 CPU 자원, 디스크, 메모리 등의 사용 할당량이 커집니다.   
   
   2. 하이퍼바이저형 서버 가상화   
   호스트 OS없이 하드웨어를 직접 제어합니다. 하드웨어 상에 가상화를 전문으로 하는 소프트웨어인 '하이버파이저'를 배치하고, 하드웨어와 가상환경을 제어합니다. 대표적으로 Microsoft Windows Server의 'Hyper-V'나 Citrix사의 'XenServer'등이 있습니다.   

1. # 도커의 3가지 기능

   애플리케이션이 가동 시키기 위한 조건   
   1.애플리케이션의 실행 모듈(프로그램 본체)   
   2.미들웨어나 라이브러리 군   
   3.OS/네트워크 등과 같은 인프라 환경   

   2. 이미지를 만드는 기능(Build)   
   애플리케이션의 실행에 필요한 프로그램 본체, 라이브러리, 미들웨어, OS나 네트워크 설정 등을 하나로 모아서 Docker 이미지를 만듭니다. Docker에서는 하나의 이미지에는 하나의 애플리케이션만 넣어 두고, 여러 개의 컨터이너를 조합하여 서비스를 구축하는 방법을 택합니다. Docker 이미지의 정체는 애플리케이션의 실행에 필요한 디렉토리입니다.   

   2. 이미지를 공유하는 기능(Ship)   
   Docker 이미지는 Docker 레지스트리에서 공유할 수 있습니다. Docker의 공식 레지스트리는 Docker Hub입니다. 여기에는 다양한 Docker 이미지들이 제공되고 있는데, 여기에서 Ubuntu나 CentOS와 같은 Linux이미지를 설치 후 여기에 미들웨어나 라이브러리, 전개 할 애플리케이션 등을 넣은 이미지를 겹쳐서 설치가 가능합니다.   

   2. 컨테이너를 작동시키는 기능   
   Linux 상에서 컨테이너 단위로 서버 기능을 작동시킵니다. 이 컨테이너의 바탕이 되는 것이 Docker 이미지입니다. 이미지만 있으면 Docker가 설치된 환경은 어디서든 컨테이너를 작동시킬 수 있습니다. 또한 하나의 Docker 이미지로 여러개의 컨테이너를 실행시킬 수 있습니다.   

1. 이미지 변조 방지 및 취약성 검사   

   Docker Container Trust    
   Docker Security Scanning   

1. Docker 컴포넌트
   2. Docker Engine(Docker의 핵심 기능)   
   Docker 이미지를 생성하고 컨테이너를 기동시키기 위한 Docker의 핵심 기능입니다. Docker명령의 실행이나 Dockerfile에 의한 이미지도 생성합니다.   

   2. Docker Registry(이미지 공개 및 공유)   
   컨테이너의 바탕이 되는 Docker 이미지를 공개 및 공유하기 위한 레지스트리 기능입니다. 공식 레지스트리로 Docker Hub가 있습니다.   

   2. Docker Compose(컨테이너 일원 관리)   
   여러 갱의 컨테이너 구성 정보를 코드로 정의하고, 명령을 실행함으로써 애츨리케이션의 실행 환경을 구성하는 컨테이너들을 일원 관리하기 위한 툴입니다.   

   2. Docker Machine(Docker 실행 환경 구축)   
   Virtual Box나 아마존의 EC2, Microsoft의 Azure와 같은 클라우드 환경에 Docker의 실행 환경을 명령으로 자동 생성하기 위한 툴입니다.   

   2. Docker Swarm(클러스트 관리)   
   Docker Swarm은 여러 Docker 호스트를 클러스터화하기 위한 툴입니다. 클러스터를 관리하거나 API를 제공하는 역할은 Manager가, Docker 컨테이너를 실행하는 역할은 Node가 담당합니다.   

1. # 컨테이너를 구획화하는 장치(namespace)
   Docker는 컨테이너라는 독립된 환경을 만들고, 그 컨테이너를 구획화하여 애플리케이션의 실행 환경을 만듭니다. 이 컨테이너를 구획하는 기술은 Linux 커널의 namespace라는 기능을 사용하고 있습니다. 한 덩어리의 테이블에 이름을 붙여 분할함으로써 충돌 가능성을 줄이고, 쉽게 참조할 수 있게 하는 개념입니다.   

   2. PID namespace   
   PID란 Linux에서 각 프로세스에 할당된 고유한 ID를 말합니다. PID namespace는 PID와 프로세스를 격리시킵니다. namespace가 다른 프로세스끼리는 서로 액세스할 수 없습니다.   

   2. Network namespace   
   네트워크 디바이스, IP주소, 포트 번호, 라우팅 테이블, 필터링 테이블 등과 같은 네트워크 리소스를 결리된 namespace마다 독립적으로 가실 수 있습니다. 호스트 OS상에서 사용 중인 포트가 있더라도 컨테이너 안에서 동일한 번호의 포트를 사용할 수 있습니다.   

   2. UID namespace   
   UID(사용자 ID), GID(그룹 ID)를 namespace별로 독립적으로 가질 수 있습니다. namespace 안과 호스트OS상의 UID/GID가 서로 연결되어 namespace 안과 밖에서 서로 다른 UID/GID를 가질 수 있습니다.   

   3. MOUNT namespace   
   Linux에서 파일시스템을 사용하기 위해선 마운트가 필요합니다. 마운트란 기기나 기억장치를 OS에 인식시켜 이용가능한 상태로 만드는 것입니다. 마운트를 하여 namespace안에 격리된 파일 시스템 트리를 만듭니다.   

1. # 릴리스 관리 장치(cgroups)   
   Docker에서는 호스트 컴퓨터 자원을 여러 컨테이너가 공유하여 작동하게 되는데 이 때, 자원을 공유할 때 Linux 커널의 control groups(cgroups)기능을 사용하여 자원의 할당 등을 관립합니다. Linux에서는 프로그램을 프로세스로서 실행합니다. 프로세스는 하나 이상의 스레드 모임으로 움직입니다. cgroups는 프로세스와 스레드를 구룹화하여, 그 그룹 안에 존재하는 프로세스와 스레드에 대한 관리를 수행하기 위한 기능입니다. cgroups는 컨테이너 안의 프로세스에 대해 자원을 제한함으로써 그룹별로 자원 제한을 두어 어떤 컨테이너가 호스트 OS의 자원을 모두 사용해 버려서 다른 컨테이너에 영향을 주는 일을 막을 수 있습니다.   
   cgroups는 계층 구조를 사용하여 프로세스를 그룹화아혀 관리할 수 있습니다. cgroups의 부모자식 관계에서는 자식이 부모의 제한을 물려받습니다. 예를 들어 자식이 부모의 제한을 초과하는 설정을 하더라도 부모 cgroups의 제한에 걸립니다.   
   
1. # registry
   -registry란?   
   도커에서 레지스트리는 도커 이미지를 저장하고 공유하기 위한 중앙 저장소입니다. 레지스트리는 도커 이미지를 관리하며, 이를 통해 이미지를 빌드, 배포, 검색 및 다운로드할 수 있습니다. 도커 허브(Docker Hub)는 도커의 공식 레지스트리로, 다양한 공개 이미지들이 저장되어 있습니다. 도커 허브 이외에도 독립적으로 사설 레지스트리를 구축하거나, 다른 레지스트리 서비스를 사용할 수도 있습니다.   
   
   -사설 registry   
   도커에서 사용할 수 있는 사설 레지스트리는 다음과 같습니다:   
   
   1)도커 프라이빗 레지스트리(Docker Private Registry): 도커 공식 레지스트리인 도커 허브와 유사한 기능을 제공하는 사설 레지스트리입니다. 독립적으로 운영할 수 있으며, 보안과 접근 제어를 자체적으로 관리할 수 있습니다.   
   
   2)아티팩토리(Artifactory): 지속적인 통합 및 배포를 위한 플랫폼으로, 도커 이미지 저장소 역할을 수행할 수 있습니다. 사설 레지스트리로 사용할 수 있으며, 다양한 빌드 도구와 통합되어 사용됩니다.   
   넥서스(Nexus Repository): 소프트웨어 개발과 관련된 다양한 아티팩트를 저장하는 플랫폼으로, 도커 이미지 저장과 관리를 위한 사설 레지스트리로 사용할 수 있습니다.   
   
   3)하버(Harbor): 오픈 소스 기반의 컨테이너 레지스트리로, 도커 이미지 저장과 보안 기능을 제공합니다. 다양한 인증 및 접근 제어, 복제 및 복구, 이미지 스캐닝 등의 기능을 지원합니다.   
   이 외에도 다양한 사설 레지스트리 솔루션이 있으며, 기업이나 조직의 요구 사항에 따라 선택하여 사용할 수 있습니다.   