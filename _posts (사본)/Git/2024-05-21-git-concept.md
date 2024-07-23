---
layout: single
title: 개념
categories: Git
tag: [github, 폴더]
---

1. # 공간
   1. Working Directory   
      작업을 하고 있는 로컬 컴퓨터의 공간   

   1. Staging Area   
      커밋할 파일에 대한 정보를 저장   

   1. Git Directory   
      커밋 후 영구적으로 저장되는 스냅샷 공간

1. # origin
   초기 github를 생성시 init명령을 하게 되면   
   ```
      Initialized empty Git repository in C:/programming/source
   ```   
   이렇게 로컬의 repository가 설정됩니다. 
   
   이후 
   ```
      git remote add origin "https://github.com/nati/java.git"
   ```   
   이렇게 origin 이후에 깃허브 주소를 입력하게 됩니다.   
   
   이때 C:/programming/source인 C드라이브의 디렉토리가 로컬의 저장소인 repository가 되고, 
   
   깃허브 위치인 "https://github.com/nati/java.git"가 깃의 저장소가 되며 다른 말로 origin이 됩니다. 즉 origin은 깃의 온라인 저장소입니다.   

1. # add
   작업 중인 파일을 Working Directory에서 Staging Area로 파일 복사.   
   '복사'기 때문에 Working Directory에 있는 파일을 수정해도 Staing Area에 있는 파일은 영향을 받지 않습니다. 그렇기 때문에 파일을 수정하면 다시 add를 해줘야 합니다.

1. # commit
   git은 버전 관리를 할 때 각 버전의 '차이점'을 저장하는 것이 아니라 각각의 시점 전체를 하나의 '스냅샷' 형태로 저장하고 이 스냅샷을 만드는 과정을 커밋이라 합니다.   
   add 후 Staing Area에 있는 파일을 로컬의 Git 저장소에 저장하는 명령어.   

   - 커밋 메세지나 내용을 변경하고 싶은 경우 amend 명령어 사용   
   ```s
      git commit --amend -m "chnage msg"
   ```    
   기존 커밋을 변경하고 싶은 경우 add 후 git commit --amend   
   <span style="color:red">*한번 커밋된 파일은 수정이 불가능 합니다. amend는 첫 번째 커밋을 수정하는 것이 아니라 덮어쓰게 됩니다.</span>
   
1. # fetch
   원격 저장소에 있는 데이터를 로컬 저장소로 가져 옵니다.   

1. # merge
   fetch로 가지고 온 데이터를 합치는 일. 원격 저장소 데이터와 로컬 저장소 데이터를 합치기 위해서는 공통적인 commit부분이 있어야 합니다.   
   
1. # pull
   pull = fetch + mrege   
   
1. # upstream과 downstream
   origin(깃허브 저장소) - upstream   
   local(로컬 저장소) - downstream   

   origin → local : pull   
   local → origin : push

   origin(상위개념) - upstream   
              ↓   
   local(하위개념) - downstream   

1. # Fork
   협업이나 오픈소스 프로젝트에 참여할 때 다른 사람의 repository 파일을 자신의 깃허브로 복사는 일   
   
