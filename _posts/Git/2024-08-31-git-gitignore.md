---
layout: single
title: gitignore 설정
categories: Git
tag: [github, 폴더]
---

1. # gitignore
   gitignore는 앞으로의 파일에 대한 버전관리 규칙입니다. 그렇기 때문에 gitignore에 파일이나 디렉토리를 추가했다고해서 이미 github에 올라와서 버전관리가 되고 있는 파일이나 디렉토리가 삭제되지 않습니다. gitignore에 데이터를 추가하는 행위는 버전관리 대상에서 제외하는 의미이지 추가된 파일을 __삭제__ 하는 것은 아닙니다.   

   1.git rm으로 파일 삭제   
      ```cs
         git rm -r <폴더명 또는 파일명>
         git commit -m "삭제된 파일 커밋"
         git push
      ```   
      주의!! rm 명령은 로컬에 있는 파일을 먼저 삭제합니다. 삭제된 파일은 복구할 수 없으므로 주의해야 합니다.   
      rm으로 로컬에 있는 파일을 먼저 삭제 후 원격저장소와 동기화합니다.   

      ```cs
         git rm -r aa/aa.txt //aa디렉토리에 aa.txt파일 삭제
         git rm -r aa/bb     //aa디렉토리에 bb디렉토리와 하위 디렉토리 모든 삭제

         //예제)
         natis@WIN11_DATA MINGW64 /c/khj/test (main)
         $ git rm -r "aa/bb"
         rm 'aa/bb/bb.txt'
         rm 'aa/bb/cc/cc.txt'
      ```

   2.로컬에서 직접 파일 삭제 후 commit -> push   

   3.깃허브에서 직접 파일 삭제 후 pull   

1. # 슬래쉬 방향
   windows에서 폴더 경로를 지정시 백슬래쉬`(\)`를 사용하고 linux에서는 `/`를 사용하지만 gitignore 안에 경로 설정은 windows나 linux 구분없이 `/`를 사용합니다.   

1. # 디렉토리와 파일 추가

   ```cs
      /target  //target 디렉토리와 그 하위 모든 디렉토리 및 파일을 버전 관리에서 제외
      target/  //target 디렉토리와 그 하위 모든 디렉토리 및 파일을 버전 관리에서 제외
      /target/ //target 디렉토리와 그 하위 모든 디렉토리 및 파일을 버전 관리에서 제외
      
      finename.txt //특정 파일 하나만 버전 관리 제외

      target/filename.txt //target디렉토리 안에 filename.txt만 버전 관리 제외
      /target/filename.txt //target디렉토리 안에 filename.txt만 버전 관리 제외

      *.xml //xml 확장자를 가진 모든 파일 차단

      **/target/ //어떤 경로에 있던 target디렉토리와 그 하위 디렉토리를 버전 관리에서 제외

      target  ////어떤 경로에 있던 target 이름의 디렉토리, 파일과 그 하위 디렉토리를 버전 관리에서 제외
   ```
   `/target` 과 `target/` 과 `/target/` 은 각각 다른점이 있다고 하는데 직접 해본 결과 차이를 발견할 수 없었음.   
