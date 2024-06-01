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
   