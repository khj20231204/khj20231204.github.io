---
layout: single
title: 프로그램 설치/삭제
categories: Ubuntu
tag: [ssh, scp]
---

1. # 패키지 구성 명령어 configure
   ```s
      sudo dpkg --configure -a
   ```
   dpkg 패키지 관리자를 사용하여 설치되지 않은 패키지를 구성하는 명령어입니다. 이 명령은 시스템에서 설치되지 않은 패키지를 구성하고, 설치 중에 오류가 발생한 패키지를 다시 구성하여 문제를 해결하는 데 사용됩니다.

   리눅스에서 –configure는 패키지 관리자인 dpkg를 사용하여 설치되지 않은 패키지를 구성하는 명령어입니다. 이 명령어는 시스템에서 설치되지 않은 패키지를 구성하고, 설치 중에 오류가 발생한 패키지를 다시 구성하여 문제를 해결하는 데 사용됩니다. dpkg는 리눅스에서 소프트웨어 패키지를 설치, 구성, 제거하는 데 사용되는 도구 중 하나입니다.

   dpkg –configure 옵션에는 다음과 같은 하위 옵션
   -a: 모든 패키지를 구성합니다.
   패키지 이름: 특정 패키지를 구성합니다.
   –pending: 아직 구성되지 않은 패키지를 구성합니다.
   –force-confnew: 패키지 설정 파일을 기본값으로 덮어쓰기합니다.
   –force-confold: 패키지 설정 파일을 현재 값으로 유지합니다.
   –force-confdef: 패키지 설정 파일을 변경하지 않고 유지합니다.
   –force-confmiss: 패키지 설정 파일이 누락되었을 경우 복구합니다.
   –force-confask: 패키지 설정 파일에 대해 사용자에게 확인을 요청합니다.
   –force-all: 모든 패키지를 구성하고, 오류를 무시합니다.
   –no-triggers: 패키지 트리거를 실행하지 않습니다.

1. # .bundle 설치
   ```s
      chmod u +x 파일이름.bundle #.bundle 파일을 실행 가능하도록 만들어야 합니다
      ./파일이름.bundle
   ```   
   
1. # deb파일 설치
   
   dpkg 버전 확인   
   ```s
      dpkg --version
   ```

   dpkg로 deb파일 설치
   ```s
      sudo dpkg -i <파일 경로>/<파일 이름>.deb

      sudo dpkg -i /home/user/downloads/package.deb
   ```

   dpkg로 설치한 패키지 삭제
   ```s
      sudo dpkg -r <패키지 이름>   
   ```   

1. # purge
   purge는 리눅스에서 패키지 관리자를 통해 설치된 패키지와 관련된 모든 파일을 삭제하는 명령어입니다. 보통 패키지를 제거할 때 사용되며, 해당 패키지와 관련된 설정 파일, 데이터 파일, 의존성 파일 등을 모두 제거합니다.   

   purge 명령어는 주로 Debian 계열의 리눅스 배포판에서 사용되는 apt 패키지 관리자와 함께 사용됩니다. 다음은 purge 명령어의 기본적인 사용법입니다.   

   ```s
      sudo apt-get purge [패키지 이름]

      sudo apt-get purge firefox
   ```   
   위의 예시는 firefox 패키지와 관련된 모든 파일을 삭제합니다.   

   purge 명령어를 사용하면 패키지가 설치될 때 생성된 파일들을 모두 삭제할 수 있습니다. 이는 패키지를 완전히 제거하고, 다시 설치할 때 이전 설정이나 데이터의 영향을 받지 않도록 도와줍니다.   
   주의해야 할 점은 purge 명령어는 시스템 파일이나 설정 파일에 대한 변경을 수반할 수 있으므로 신중하게 사용해야 합니다.   

1. # 설치할 프로그램

   - 루비   
   쉘 스크립트로 작성   
   ```s
   #!/bin/bash

   sudo apt update && apt upgrade -y

   #ruby prerequisites
   sudo --dpkg configure -a
   sudo apt-get -y install ruby-full build-essential zlib1g-dev

   echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
   echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
   echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
   source ~/.bashrc

   #jekyll and bundler
   gem install jekyll bundle

   #Execute in blog Directory
   #bundle install
   #bundle exec jekyll serve
   ```
   
   - 프로그램   
   2. 비쥬얼 스튜디오   
   ```s
      sudo dpkg -i code_1.84.2-1699528352_amd64.deb   
   ```   
   2. VMware   
   ```
      sudo chmod +x VMware-Player-Full-16.2.5-20904516.x86_64.bundle   
      sudo ./VMware-Player-Full-16.2.5-20904516.x86_64.bundle    
   ```   
   2. 웨일
   ```
      sudo dpkg -i naver-whale-stable_amd64.deb   
   ```
   