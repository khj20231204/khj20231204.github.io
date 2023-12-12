---
layout: single
title: 압축
categories: Ubuntu
tag: [아카이브, gzip]
---

1. # 아카이브
   다수 개의 파일이나 디렉토리를 하나로 묶는 것   
   tar명령어   
   jar명령어   

1. # 옵션
   tar [옵션] [새로운파일명] [대상파일1] [대상파일2] [대상파일3]   
   → 대상파일들을 하나의 새로운파일명으로 묶어 버립니다.   

   | 옵션 | 기능 |
   |:---:|:---:|
   |c| 새로운 아카이브 tar 파일 생성 |
   |x| 묶음 해제 |
   |v| 처리하고 있는 과정 출력 |
   |f| 아카이브 장치 지정(파일 또는 백업 장치를 지정) |
   |t| 아카이브 안에 파일 목록 나열 |

   * f: f옵션 뒤에 file, tape, cd-rom등 백업할 장치 이름을 입력합니다. 리눅스는 장치도 파일이름으로 관리가 됩니다. 장치이름을 생략하고 바로 파일이름을 입력하면 file로 백업이 됩니다. 만약 f옵션을 생략하면 tar가 원래는 tape장치에 backup를 하기 위한 명령어였기 때문에 장치를 설정하지 못 해서 에러가 발생합니다.   

   ```
      tar cvf fruits.tar banana kiwi apple   'tar 파일 생성'
   ```   
   <span style="color:red">파일명 뒤에 .tar 안 붙여도 됩니다. 확장자는 단순히 파일이름입니다. 파일을 구분하는 건 안에 내용</span>   

   ```   
      [nati@localhost ~]$ tar cvf fruits2.tar /home/nati/apple /home/nati/banana /home/nati/tomato '절대 경로'
      [nati@localhost mytar]$ tar xvf fruits2.tar
      home/nati/apple
      home/nati/banana
      home/nati/tomato
      [nati@localhost mytar]$ ls
      home   '절대 경로의 디렉토리가 만들어집니다'

      [nati@localhost ~]$ tar cvf fruits1.tar apple banana tomato   '상대 경로'
      [nati@localhost mytar]$ tar xvf fruits1.tar
      apple
      banana
      tomato
      [nati@localhost mytar]$ ls
      apple  banana  fruits1.tar  tomato   '현재 디렉토리에 바로 tar해제'
   ```   
   절대경로 묶을 시 폴더경로 포함   

   ```
      tar tvf fruits.tar   'tar안에 내용 확인'

      tar xvf fruits.tar   'tar 해제'
   ```   

1. # jar명령어
   JAR(Java Archive, 자바 아카이브)는 여러개의 자바 클래스 파일과, 클래스들이 이용하는 관련 리소스(텍스트, 그림 등) 및 메타데이터를 하나의 파일로 모아서 자바 플랫폼에 응용 소프웨어나 라이브러리를 배포하기 위한 소프트웨어 패키지 파일 포맷입니다. tar앞에 t대신 j를 사용한 명령어로 tar와 동일한 동작과 옵션을 가집니다. 압축은 되지 않고 단지 파일들을 모아놓은 아카이브입니다.   

1. # 압축 

   |   |압축|압축 해제|
   |:---:|:---:|:---:|
   |zip|zip [새로운파일명] [대상파일명] | unzip [파일명]|
   |gzip|gzip [대상파일명] | gunzip [파일명]|
   |bzip2|bzip2 [대상파일명] | bunzip2 [파일명]|   
   
   *zip은 윈도우에서도 사용하는 파일 형식이기 때문에 윈도우에서 압축한 걸 리눅스에서 풀 수 있고, 리눅스에서 압축할 걸 윈도우에서 풀 수 있습니다.   
   *gzip과 bzip2는 대상파일명을 바로 입력합니다. 그렇기 때문에 파일이 여러개인 경우 먼저 tar로 묶은 후 압축을 해야 됩니다.   
   <span style="color:red">zip은 windows와 linux 서로 호환 가능</span>   

   - zip압축   
   아카이브와 압축을 한번에 실행   
   windows와 linux에서 서로 호환 가능   
   ```
      [nati@localhost mytar]$ zip fruits.zip apple banana tomato
      adding: apple (stored 0%)
      adding: banana (stored 0%)
      adding: tomato (stored 0%)
   ```   
   apple banana tomato 3개를 넣어서 하나의 frutis.zip이란 압축파일을 만듭니다. 여러 파일이나 디렉토리를 한번에 묶어서 압축을 합니다.   

   - gzip압축   
   ```
      [nati@localhost mytar]$ gzip fruits.tar
      [nati@localhost mytar]$ ls -al
      -rw-rw-r--.  1 nati nati   153 Aug 15 05:39 fruits.tar.gz
   ```   
   gzip [파일명] 파일명.gz 형태로 압축 파일을 만듭니다. 그렇기 때문에 보통 tar로 묶어서 하나의 파일로 만든 후 gzip을 수행합니다. 새로운 파일을 만든는 것이 아니라 압축한 파일 자체가 .gz로 만들어집니다.   
   
   - bzip2압축      
   ```
      [nati@localhost mytar]$ bzip2 fruits.tar
      [nati@localhost mytar]$ ls -al
      -rw-rw-r--.  1 nati nati  170 Aug 15 05:39 fruits.tar.bz2
   ```   
    bzip2 [파일명] 파일명.bz2 형태로 압축 파일을 만듭니다. 그렇기 때문에 보통 tar로 묶어서 하나의 파일로 만든 후 bzip2을 수행합니다. 새로운 파일을 만든는 것이 아니라 압축한 파일 자체가 .bz2로 만들어집니다.   

1. # 압축 해제

   - unzip   
      ```
         [nati@localhost mytar]$ unzip fruits.zip
         Archive:  fruits.zip
         extracting: apple                   
         extracting: banana                  
         extracting: tomato                  

         [nati@localhost mytar]$ ls -al
         -rw-rw-r--.  1 nati nati    0 Aug 15 04:49 apple
         -rw-rw-r--.  1 nati nati    0 Aug 15 04:49 banana
         -rw-rw-r--.  1 nati nati  440 Aug 15 05:49 fruits.zip
         -rw-rw-r--.  1 nati nati    0 Aug 15 04:49 tomato
      ```   
      unzip은 압축해제   

   - gunzip   
      ```
         [nati@localhost mytar]$ ls
         fruits.tar.gz 
         [nati@localhost mytar]$ gunzip fruits.tar.gz    'gunzip은 압축만 품'
         [nati@localhost mytar]$ ls 
         fruits.tar    'tar 파일로 나타남'
      ```   
      gunzip [파일명]을 하게 되면 압축만 풀기 때문에 fruits.tar 파일이 그대로 있습니다.   
      
      __tar에 z옵션으로 한꺼번에 풀기__   
      __z__ : gzip에서 압축을 하거나 해제하는 옵션   
      x : tar해제   
      v : 처리 과정 출력   
      f : 파일명 지정   

      tar __z__ xvf  
      ```
         [nati@localhost mytar]$ tar zxvf fruits.tar.gz    'tar에 zxvf 옵션으로 한꺼번에 풀기'
         apple
         banana
         tomato
         [nati@localhost mytar]$ ls
         apple  banana  fruits.tar.gz  tomato
      ```   
      g[지] z[지]   

   2. bunzip2
      ```
         [nati@localhost mytar]$ ls
         fruits.tar.bz2 
         [nati@localhost mytar]$ bunzip2 fruits.tar.bz2    'bunzip2는 압축만 품'
         [nati@localhost mytar]$ ls
         fruits.tar    'tar 파일로 나타남'
      ```   
      bunzip2 [파일명]을 하게 되면 압축만 풀기 때문에 fruits.tar 파일이 그대로 있습니다.   

      __tar에 j옵션으로 한꺼번에 풀기__   
      __j__ : bzip2로 압축을 하거나 해제하는 옵션    
      x : tar해제   
      v : 처리 과정 출력   
      f : 파일명 지정   

      tar __j__ xvf [파일명]   
      ```
         [nati@localhost mytar]$ ls
         fruits.tar.bz2
         [nati@localhost mytar]$ tar jxvf fruits.tar.bz2    'tar에 jxvf 옵션으로 풀기'
         home/nati/apple
         home/nati/banana
         home/nati/tomato
         [nati@localhost mytar]$ ls
         fruits.tar.bz2  home    'home안에 apple, banana, tomato 해제됨'
      ```   
      *bj

1. # 정리

   tar 묶기 : tar cvf [새로운파일명] [묶을파일이름나열..]   
   tar 해제 : tar xvf [묶음풀파일명]   
   zip 압하기 : zip [새로운파일명] [압축할파일나열..]   
   zip 해제 : unzip [압축풀파일명]   
   gzip 한번에 압축 : tar zcvf [새로운파일명] [묶을파일이름나열..]   
   gzip 한번에 해제 : tar zxvf [압축풀파일명]   
   bzip2 한번에 압축 : tar jcvf [새로운파일명] [묶을파일이름나열..]   
   bzip2 한번에 해제 : tar jxvf [압축풀파일명]   
 
   *확장자를 적지 않아도 압축과 해제하는데 상관없지만 확장자가 있어야 파일을 구별할 수 있음   