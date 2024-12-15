---
layout: single
title: 리눅스 명령어
categories: DEV(Lesson)
tag: []
author_profile: false
---

리눅스 명령어

o 가상화면   
Ctrl + Alt + F1 ~ F6   
Ctrl + Alt + F7  : GUI 화면으로 복귀   

o whoami : 현재 계정명  
$ whoami   
myubuntu   

o pwd : 현재 작업 디렉토리명   
$ pwd   
/home/myubuntu   

o 리부팅   
$ reboot   
$ init 6   
$ shutdown -r now   

o 시스템 종료   
$ sudo halt   
$ sudo init 0   
$ sudo shutdown -h now   

o ifconfig : ip주소 확인   
$ ifconfig   
 inet addr:192.168.130.128   

o ifconfig설치   
   sudo apt update   
   sudo apt install net-tools   

o ping : 네트워크 점검용 명령어   
$ ping  kbs.co.kr   

o docker 에서 ping 설치   
sudo apt-get install iputils-ping   

o 열린 포트 확인   
   sudo ss -tuln | grep 80 - 목록에 80이 나타나면 열려있는 것   

o 방화벽 상태 확인   
   sudo ufw status   
      Status : active - 방화벽 활성화된 상태   
      Status : inactive - 방화벽 비활성화된 상태   

o 방화벽 실행   
   sudo ufw enable   

o 방화벽 비활성화   
   sudo ufw disable   

o 특정 포트 열기   
   sudo ufw allow 80/tcp - 일반적으로 http, https는 tcp 사용   

cf. sudo 를 붙이면 root 권한을 가지게 된다.   

o ls : 현재 디렉토리의 파일 및 디렉토리 출력   
$ ls   
$ ls -l : 자세하게 목록 출력   
$ ls -a : 히든파일도 출력   
$ ls -al : 모든 파일을 자세하게 출력   
$ ll : 모든 파일을 자세하게 출력   

o cd : 디렉토리 변경   
$cd  /  : 최상위 디렉토리(/)로 변경   
$cd  home : home 디렉토리로 변경   
$cd  /tmp : tmp 디렉토리로 변경   
$cd      : 자신의 계정 디렉토리로 변경   
$cd  ~  : 자신의 계정 디렉토리로 변경   
$cd  ..   : 한단계 상위 디렉토리로 변경   

o clear : 화면 정리   
$clear   

o ubuntu 리눅스의 디렉토리 구조   
bin : 일반명령어 파일 파일이 있는 디렉토리   
boot : 부팅에 필요한 파일이 있는 디렉토리   
etc : 설정파일들이 모여있는 디렉토리   

$ vi /etc/passwd : 계정 정보   
$ sudo vi /etc/shadow : 비밀번호 정보   
cdrom : 외부 장치와 연결할때 사용하는 디렉토리   
dev : 장치 정보 디렉토리   
home : 계정 디렉토리 /home/myubuntu   
root : root 계정 디렉토리   
sbin : 리눅스 관리자가 사용하는 명령어 디렉토리   
tmp : 임시 디렉토리   
usr : 프로그램이 설치 디렉토리 - 설치 시 여기에 프로그램 저장   
var : 가변적인 데이터가 저장되는 디렉토리   
      로그 파일(web log, ftp log, mail log 파일)   

o mc   
mc 설치   
$ sudo apt-get update
$ sudo apt-get install mc  //모든 명령어는 앞에 f를 넣어서 클릭, 1=>f1버튼, 2=>f2버튼, 3=>f3버튼 

mc 실행   
$ mc   

o cp : 파일, 디렉토리 복사   
cp 원본파일 타켓디렉토리   

o mv : 파일, 디렉토리 이동   
mv 원본파일 타켓디렉토리   

o mv : 파일명 변경   
mv 원본파일명 변경할파일명   
ex)mv test test.java   

o mkdir : 디렉토리 생성   
$mkdir test : test 디렉토리 생성   

o rmdir : 디렉토리 삭제(비어있는 디렉토리만 삭제됨)   
$rmdir test : test 디렉토리 삭제   

o rm : 파일 또는 디렉토리 삭제   
$rm test     : test 디렉토리 삭제   
$rm -r test  : 내용이 있는 디렉토리 삭제   

o whereis : 명령어 위치 찾아주는 명령   
$ whereis  ls   
$ whereis  mc   
/usr/bin/mc   

o 리눅스 편집 프로그램   
vi 편집기   
emacs   
nano   
gedit  : GUI 편집 프로그램   

o docker에서  설치   
 # apt-get  install  vim   
 # apt-get  install  nano   

O vi editor   
- 명령모드 : 편집, 수정    
yy(복사), dd(삭제), p(붙이기)   

- 입력모드 :  a, i, o키 누르면 입력모드로 전환됨   

- 콜론모드   
:set nu (줄번호 표시)   
:set nonu (줄번호 삭제)   
:w (저장)   
:q (종료)   
:wq(저장후 종료)   

vi editor 실습   
$cd  /tmp   
$ vi  test   

$ nano  test   

$ gedit  test   


o 계정 생성   
$ sudo  adduser   생성할계정명   
$ sudo  adduser   test   
passwd :  1234   
repasswd : 1234   

/home/test  계정 디렉토리 생성됨   
vi  /etc/passwd  파일에 계정정보가 저장된다.   
sudo  vi  /etc/shadow  비밀번호가 암호화 되어서 저장   

o 비번설정   
$ sudo passwd  계정명   
$ sudo passwd  test   
passwd :  12345   
repasswd : 12345   

o 계정 전환   
$ su  전환할계정명   

o myubuntu 계정에서 test 계정으로 계정전환   
$ su   test       : test 계정으로 전환   
passwd : 12345    
$ whoami          : 현재 계정명 확인   
test   

o root 계정 비밀번호 설정 : 1234   
$ su  myubuntu   
$ sudo  passwd  root   
passwd :       => 현재 계정의 비번입력   
passwd : 1234  => root 계정의 비번입력   
repasswd : 1234   

o myubuntu 계정에서 root 계정으로 계정전환   
2가지 방법 모두 사용 가능   
$ su root :    
$ su  -   
passwd : 1234 => root 계정의 비번입력   

#whoami   
root   

o root 계정에서 myubuntu 계정으로 계정전환   
su  myubuntu   : 비번을 물어보지 않고 계정전환됨   

o 허가권(permission)   
$ ls -al   
rwx &nbsp;&nbsp;   rwx   rwx   
소유자권한 소유그룹권한 타인의권한   

r : read (읽기)   4   
w : write (쓰기)  2   
x : execute (실행)1   

1 - 실행   
2 - 쓰기   
3 - 실행,쓰기   
4 - 읽기   
5 - 실행, 읽기   
6 - 쓰기, 읽기   
7 - 실행, 쓰기, 읽기   

o 허가권 변경
$ chmod 777 파일 or  폴더명   
755   

$ cd  /home   
$ sudo  chmod   755   myubuntu   -R   
*-R : 하위 디렉토리까지 755로 적용됨   

o  소유자, 소유그룹 변경   
 $ chown  소유자.소유그룹   파일 or 폴더   -R   
 $ chown   root.root   toto   


