---
layout: single
title: 컴파일로 프로그램 설치
categories: Ubuntu
tag: []
---


1. 필요한 빌드 도구 설치: 컴파일을 위해 필요한 도구를 설치해야 합니다. 다음 명령을 사용하여 필수 패키지를 설치할 수 있습니다.   
```
   //Ubuntu
   sudo apt-get install build-essential

   //CentOS
   sudo yum groupinstall "Development Tools"
```   

1. 소스 코드 다운로드: 컴파일할 소스 코드를 다운로드합니다. 소스 코드는 일반적으로 .tar.gz 또는 .zip 형식으로 제공됩니다.   

1. 압축 해제: 다운로드한 소스 코드를 압축 해제합니다. 압축 해제는 일반적으로 다음 명령으로 수행할 수 있습니다.   
```
   tar -xzvf 파일이름.tar.gz
```   

1. 디렉토리 이동: 압축 해제된 디렉토리로 이동합니다.   

1. 컴파일 및 설치: 컴파일 및 설치를 위해 다음 명령을 사용합니다.   
```
   ./configure
   make
   sudo make install
```   

위 단계를 따라가면 컴파일된 파일이 시스템에 설치됩니다. 컴파일 과정에서 필요한 추가 의존성 패키지가 필요한 경우, 해당 패키지도 설치해야 할 수 있습니다. 컴파일된 파일은 보통 /usr/local/bin/ 또는 /usr/local/lib/ 등의 경로에 설치됩니다.   