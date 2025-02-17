---
layout: single
title: 프로그램 삭제하기
categories: Ubuntu
tag: 
---

1. # APT(패키지 관리자)로 설치된 경우
   APT로 설치된 패키지는 우분투 공식 저장소에서 내려받아 설치됩니다.   

   🔎 설치 여부 확인   
   ```bash
      dpkg -l | grep 패키지명
   ```   
   또는   e
   ```bash
      apt list --installed | grep 패키지명
   ```   
   ✔ 위의 검색으로 출력이 있다면 APT로 설치된 것입니다.   

   🗑 삭제 방법   
   ```bash
      sudo apt remove 패키지명  # 프로그램만 삭제
      sudo apt purge 패키지명   # 설정 파일까지 삭제
      sudo apt autoremove       # 불필요한 패키지 정리
   ```

1. # DEB 패키지(.deb 파일)로 설치된 경우
   DEB 파일을 수동으로 다운로드하여 dpkg를 이용해 설치했을 경우 확인하는 방법입니다.   

   🔎 설치 여부 확인   
   ```bash
      dpkg -s 패키지명
   ```
   ✔ Status: install ok installed가 표시되면 DEB 패키지로 설치된 것입니다.   

   🗑 삭제 방법   
   ```bash
      sudo dpkg -r 패키지명   # 패키지만 삭제
      sudo dpkg --purge 패키지명  # 설정 파일까지 삭제
   ```
   의존성 문제로 삭제가 실패하면:
   ```bash
      sudo apt --fix-broken install
      sudo apt autoremove
   ```

1. # SNAP 패키지로 설치되었는지 확인
   SNAP은 우분투에서 독립적인 패키지 관리 시스템입니다.   

   🔎 설치 여부 확인
   ```bash
      snap list | grep 패키지명
   ```   
   ✔ 출력이 있다면 Snap 패키지로 설치된 것입니다.   

   🗑 삭제 방법
   ```bash
      sudo snap remove 패키지명
   ```

1. # Flatpak으로 설치되었는지 확인
   Flatpak은 Snap과 비슷한 독립적인 패키지 관리 시스템입니다.   

   🔎 설치 여부 확인   
   ```bash
      flatpak list | grep 패키지명
   ```
   ✔ 출력이 있다면 Flatpak으로 설치된 것입니다.

   🗑 삭제 방법   
   ```bash
      flatpak uninstall 패키지명
   ```

1. # ZIP 파일/소스 코드로 설치되었는지 확인
   ZIP 파일로 설치한 프로그램은 패키지 관리 시스템과 관계없이 특정 디렉터리에 압축 해제된 형태로 존재합니다.   

   🔎 설치 여부 확인   
   1.실행 파일 위치 확인   
   ```bash
      which 패키지명
   ```    
   또는   

   ```bash
      whereis 패키지명
   ```   
   ✔ /usr/local/bin/ 또는 /opt/ 같은 디렉터리에 있다면 ZIP 또는 직접 설치 가능성이 높습니다.   

   2.수동 설치된 프로그램 찾기   
   ```bash
      ls /opt/
   ```   
   ✔ /opt/ 디렉터리에 설치된 프로그램들이 있을 수 있습니다.   

   🗑 삭제 방법
   3.설치된 경로에서 직접 제거   
   ```bash
      rm -rf /opt/프로그램폴더
   ```   

1. # AppImage로 실행되는지 확인
   AppImage는 독립 실행 파일 형태로 제공됩니다.   

   🔎 설치 여부 확인
   1.일반적으로 .AppImage 파일을 직접 다운로드하여 실행하므로, /home/사용자/다운로드 폴더 등에 존재할 가능성이 높습니다.   
   2.실행 파일을 검색하려면:   
   ```bash
      find ~/ -name "*.AppImage"
   ```

   🗑 삭제 방법   
   ```bash
      rm -f 프로그램.AppImage
   ```

1. # 정리: 프로그램이 어떤 방식으로 설치되었는지 확인하는 방법   

   | 설치 방법  |  확인 명령어 | 삭제 명령어 |
   |:---------:|:-----------:|:----------:|
   | APT (apt install) | dpkg -l | grep 패키지명 |
   | DEB (dpkg -i 파일.deb) | dpkg -s 패키지명 | sudo dpkg -r 패키지명 |
   | Snap (snap install) | snap list | grep 패키지명 |
   | Flatpak (flatpak install) | flatpak list | grep 패키지명 |
   | ZIP/수동 설치 | which 패키지명 또는 find ~/ -name 패키지명 | rm -rf /경로/폴더명 |
   | AppImage | `find ~/ -name "*.AppImage"` | rm -f 프로그램.AppImage | 







