---
layout: single
title: Package
categories: Ubuntu
tag: [package, configure]
---

1. # package?
   소프트웨어의 설치, 관리, 업데이트, 제거를 쉽게 할 수 있도록 제공해주는 파일들의 묶음입니다. 우분투에선 APT(advanced Pacakge Tool)을 기반으로 하고 있습니다. apt를 사용하면 의존성 문제를 해결해주고, 패키지 간의 충돌을 방지하여 소프트웨어 관리를 편리하게 할 수 있습니다. 우분투에서 패키지는 일반적으로 .deb 확장자를 가지는 디비안 패키지 형식을 사용합니다.   

1. # 형식
   
   2. Red Hat 계열   
   배포판: Red Hat Enterprise Linux, CentOS, Fedora   
   
   2. Debian 계열   
   배포판 : Debian GNU/Linux, Ubuntu   ​

   CentOS와 Ubuntu   

   | CentOS  | Ubuntu | 기능 |
   |:-------:|:------:|:-------:|
   |   yum   |   apt  | 패키지 관리<br>yum은 rpm을 기반, apt는 dpkg를 기반<br>의존성 문제 자동 해결 |
   |   rpm   |  dpkg  | 패키지 관리<br>의존성 문제 직접 해결 |
   |   wget  |  curl  | HTTP, HTTPS, FTP 프로토콜을 사용하여 파일을 다운로드<br>→인터넷 주소로 다운로드 |

   *wget과 curl은 CentOS, Ubuntu 구별없이 사용 함
      
   2. yum 명령어   
   Red Hat 계열 패키지 관련 명령어   
   rpm 이라는 패키지 파일을 관리하는 시스템이 RPM(Redhat Package Manager)   
   rpm 명령어를 쉽게 사용할 수 있도록 만든 명령어가 yum   
   패키지간 의존성 자동 해결(기존 패키지 알아서 설치)   
   ex)yum install <패키지 이름>   
   yum earse /remove <피키지 이름>   
   yum search <검색 키워드>   
   yum info <패키지 이름>   

   2. apt 명령어   
   Debian 계열 패키지 관련 명령어   
   deb라는 패키지 파일을 관리하는 명령어가 dpkg   
   dpkg 명령어를 쉽게 사용할 수 있도록 만든 명령어가 apt   
   패키지간 의존성 자동 해결(기존 패키지 알아서 설치)   
   ex)sudo apt-get install <패키지 이름>   
   sudo apt-get remove <패키지 이름> : 설정 파일과 같은 일부 파일이 시스템에 남게 됨   
   sudo apt-get purge <패키지 이름> : 설정 파일 포함 전부 제거   
   sudo apt-cache search <검색 키워드> : 패키지 검색   
​
1. # package 관리 도구
   2. __dpkg(Debian Package)__ - apt이전에 사용한 관리도구입니다. 패키지를 직접 다루기 때문에 패키지 간의 의존성 문제를 자동으로 해결해주지 못합니다. 의존하는 패키지가 필요한 경우 사용자가 직접 수동으로 설치해야 합니다. 또한 dpkg는 인터넷 상의 저장소로부터 직접 다운로드 하지 않으며, 로컬에 이미 다운된 패지지 파일을 사용합니다.   
   
   2. __apt__ - apt는 Advanced Package Tool의 약자로 dpkg를 기반으로 하지만 의존성 문제를 자동으로 해결할 수 있습니다. 인터넷의 저장소로부터 다운로드하고 설치, 업데이트, 제거 등의 작업을 수행합니다. apt는 apt-get, apt-cache, apt-add-repository 등의 명령어를 제공합니다.   
   apt-get : 패키지를 설치, 업데이트, 제거의 작업을 합니다.   
   apt-cache : 패키지 정보를 검색하고 조회하는 데 사용됩니다.   
   apt-add-repository : 새로운 저장소를 시스템에 추가할 때 사용됩니다.   

1. # package 설치 장소?
   패키지 관리자를 통해 설치하면 패키지는 시스템의 특정 디렉토리에 설치됩니다. 이 디렉토리는 배포판 및 패키지 관리자에 따라 다를 수 있지만, 일반적으로 /usr/bin, /usr/lib, /usr/include 등의 디렉토리에 설치됩니다. 이 디렉토리는 시스템 전체에 공유되는 패키지 파일들이 저장되는 곳입니다.   
   또한, 사용자가 직접 소스코드를 컴파일하여 생서된 실행파일이나 라이브러리 파일들은 usr/local/bin, usr/local/lib, usr/local/include 등의 디렉토리에 설치될 수 있습니다. 이 디렉토리들은 사용자가 컴파일한 소스 코드를 통해 생성된 패키지 파일들이 저장되는 곳 입니다.   

1. # package 목록 확인   
   package목록은 2가지로 검색이 가능합니다. 1)저장소에 등록된 패키지 목록 과 2)로컬 시스템에 설치된 패키지 목록 입니다.   
   apt search와 apt list는 우분투에서 패키지를 검색하고 목록을 보여주는 두 가지 *다른 명령어*입니다.   
   2. __apt search:__ *저장소* 에 등록된 패키지들을 검색하여 사용자가 입력한 키워드와 관련된 패키지를 찾아줍니다. 검색 결과로 패키지의 이름, 설명 등을 보여줍니다. 이 명령어는 패키지를 설치하기 전에 원하는 패키지를 찾는 데 사용됩니다.   
   2. __apt list:__ *시스템에 설치된* 패키지들의 목록을 보여줍니다. 기본적으로는 시스템에 설치된 모든 패키지를 보여주지만, 옵션을 사용하여 필요한 정보만 표시하거나 특정 패키지를 확인할 수도 있습니다. 이 명령어는 시스템에 설치된 패키지들을 관리하고 업데이트할 때 유용합니다.   
   따라서, apt search는 패키지를 검색하고 찾는 데에 사용되며, apt list는 시스템에 설치된 패키지들을 확인하고 관리하는 데에 사용됩니다.   
   2. __로컬에 설치된 패키지의 버전과 저장소의 최신 버전을 비교__   
   ```s
      apt list --upgradable
   ```   
   이 명령어는 업그레이드 가능한 패키지 목록을 표시합니다.   

   2. 패키지로 설치된 항목   
   ```s
      apt list --installed
   ```

1. # package 목록 파일 위치
   우분투에서 패키지 목록은 /var/lib/apt/lists/ 디렉토리에 저장되어 있습니다. 이 디렉토리는 우분투의 다양한 저장소에서 제공하는 패키지에 대한 정보가 포함된 파일들이 있습니다. 패키지 목록 파일은 .list 확장자를 가지며, 저장소마다 별도의 파일이 생성됩니다. 패키지 목록은 시스템이 업데이트되거나 새로운 패키지가 추가될 때마다 자동으로 업데이트됩니다. 따라서 저장소의 패키지 정보와 로컬의 패키지 정보가 일치하도록 최신 정보를 유지하는 것이 중요합니다.   

1. # 명령어
   - 패키지 검색   
   dpkg -S file-name   
   apt list --installed | grep file-name   

   - 패키지 삭제   
   apt-get remove package-name   
   이 명령은 해당 패키지를 시스템에서 제거합니다. 연관된 파일은 삭제되지 않습니다. 만약 연관된 파일도 함께 삭제하려면 purge 명령을 사용할 수 있습니다.   
   apt-get purge package-name   
   위의 명령을 사용하여 원하는 패키지를 삭제할 수 있습니다. 패키지 이름을 알고 있다면 해당 패키지만 삭제하고 다른 패키지에는 영향을 주지 않습니다.   

   - 패키지 재구성
   dpkg –configure -a
   Ubuntu 시스템에서 패키지 구성을 재설정하는 명령어입니다. 이 명령어를 사용하면 설치된 패키지 중에서 구성이 완료되지 않은 것들을 다시 구성할 수 있습니다. 일반적으로 시스템 업데이트나 패키지 설치 중에 구성 오류가 발생하여 패키지가 올바르게 설치되지 않았을 경우 이 명령어를 사용하여 문제를 해결할 수 있습니다. “dpkg –configure -a” 명령어를 실행하면 구성되지 않은 모든 패키지들이 자동으로 구성되며, 설치가 완료됩니다. 하지만 이 명령어를 사용하기 전에 주의해야 합니다. 시스템 업데이트 중에 구성 오류가 발생한 경우에만 사용해야 하며, 무분별한 사용은 시스템 안정성에 영향을 줄 수 있습니다. 따라서 이 명령어를 사용하기 전에 문제의 원인을 파악하고, 문제를 해결할 수 있는 다른 방법을 찾는 것이 좋습니다.

1. # 패키지 목록 파일 예
   패키지 목록 파일은 .list 확장자를 가지며, 저장소마다 별도의 파일이 생성됩니다.   
   ex)archive.ubuntu.com_ubuntu_dists_bionic_main_binary-amd64_Packages   
   archive.ubuntu.com 저장소에서   
   bionic 버전의   
   main 섹션에서 제공되는   
   amd64 아키텍처의   
   이진 파일(packages) 입니다.   

1. # 저장소의 패키지 인터넷 주소 확인
   /etc/apt/sources.list 파일을 열면 여러 줄로 구성된 텍스트를 볼 수 있습니다. 각 줄은 저장소의 주소와 속성을 지정하는데 사용됩니다. 주석 처리된 줄은 # 문자로 시작하며, 주석 처리된 줄은 저장소 구성에 영향을 주지 않습니다. 일반적으로 주석 처리되지 않은 줄에는 deb 또는 deb-src라는 키워드가 포함되어 있습니다. deb는 이진 파일 패키지를 제공하는 저장소를 나타내고, deb-src는 소스 코드 패키지를 제공하는 저장소를 나타냅니다.   
   형식 : deb [주소] [분류] [구성]   
   여기서 [주소]는 저장소의 인터넷 주소를 나타내며, [분류]는 저장소의 구분을 나타내는 문자열입니다. [구성]은 저장소의 구성을 나타내는 문자열로, 주로 main, universe, restricted, multiverse 등으로 지정됩니다. 예를 들어, http://archive.ubuntu.com/ubuntu bionic main은 http://archive.ubuntu.com/ubuntu 주소의 bionic 버전에서 main 구성을 제공하는 저장소를 의미합니다.   

1. # 패키지 주소와 미러 사이트 주소
   우분투에서 패키지 저장소 주소와 미러 사이트 주소는 유사한 개념이지만 약간의 차이가 있습니다.    
   __패키지 저장소 주소__ 는 패키지 관리자인 apt가 패키지를 다운로드하고 설치하는 데 사용하는 인터넷 주소입니다. 저장소 주소는 패키지의 이진 파일이나 소스 코드가 호스팅되는 서버의 주소를 나타내며, 패키지 목록과 패키지 파일에 대한 정보를 제공합니다.      
   __미러 사이트 주소__ 는 우분투의 공식 저장소를 복제한 여러 개의 서버 중 하나를 가리킵니다. 미러 사이트는 동일한 패키지를 제공하는 다른 서버로, 지리적으로 가까운 미러를 사용하면 패키지 다운로드 속도를 향상시킬 수 있습니다. 또한, 만약 공식 저장소 주소가 다운되거나 문제가 발생할 경우, 미러 사이트 중 하나를 선택하여 여전히 패키지를 다운로드할 수 있습니다. 일반적으로 우분투 설치 시에는 공식 저장소 주소가 기본 설정되며, 이는 http://archive.ubuntu.com/ubuntu와 같은 형태입니다. 사용자가 /etc/apt/sources.list 파일을 수정하여 미러 사이트 주소로 변경할 수 있습니다.   

1. # 패키지 재설정
   ```s
      dpkg -configure -a
   ```
   Ubuntu 시스템에서 패키지 구성을 재설정하는 명령어입니다. 이 명령어를 사용하면 설치된 패키지 중에서 구성이 완료되지 않은 것들을 다시 구성할 수 있습니다.

   일반적으로 시스템 업데이트나 패키지 설치 중에 구성 오류가 발생하여 패키지가 올바르게 설치되지 않았을 경우 이 명령어를 사용하여 문제를 해결할 수 있습니다. “dpkg –configure -a” 명령어를 실행하면 구성되지 않은 모든 패키지들이 자동으로 구성되며, 설치가 완료됩니다.

   하지만 이 명령어를 사용하기 전에 주의해야 합니다. 시스템 업데이트 중에 구성 오류가 발생한 경우에만 사용해야 하며, 무분별한 사용은 시스템 안정성에 영향을 줄 수 있습니다. 따라서 이 명령어를 사용하기 전에 문제의 원인을 파악하고, 문제를 해결할 수 있는 다른 방법을 찾는 것이 좋습니다.