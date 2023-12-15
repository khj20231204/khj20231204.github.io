---
layout: single
title: git 명령어
categories: Git
tag: [git]
---

1. # 최초 연결
   - repository를 새로 생성한 경우   
   ```s
      git init
      git add . #전체파일 add .(점)으로 표시 - local staing area
      git commit -m "first commit"   #local repository area
      git branch -M main   # main branch 생성
      git remote add origin git@github.com:khj20231204/CodingTest.git 
      git push -u origin main   # origin을 main으로 설정 
   ```   
   *주의 할 점은 __commit 이후 branch을 생성__ 해야 합니다. 먼저 로컬 repository에 데이터를 올리고 그 데이터로 branch에 최초 commit을 한번 해줘야 합니다.   
   *Support for password authentication was removed on August 13, 2021.   
   2021년 8월 이후 패스워드 인증 지원이 종료되었기 때문에 http가 아니라 ssh로 origin을 설정해 줘야 합니다.   
   *2020년 6월 인종차별과 주종 관계의 의미를 담은 용어를 제거하는 취지에서 기본 브랜치가 master에서 main으로 변경되었습니다. 하지만 git init를 하면 기본으로 설정되는 브랜치가 mater입니다. 그렇기 때문에 git branch -M main 명령으로 branch를 main으로 바꿔줘야합니다.      

   - repository가 존재하는 경우   
   ```s
      git remote add origin git@github.com:khj20231204/CodingTest.git
      git branch -M main
      git push -u origin main
   ```   

1. # origin 삭제   
   ```s
      git remote rm origin
   ```   

1. # add한 파일 취소하기
   reset명령어를 이용하면 됩니다. reset명령은 add를 해서 staging area에 있는 파일을 다시 working directory로 옮기는 역할을 합니다.   
   ```s
      git reset README.md
   ```   
1. # branch
   2. ## branch 목록확인   
   ```s
      git branch 
   ```   

   2. ## branch 생성   
   second란 이름의 branch 생성   
   ```s
      git branch second
   ```   

   2. ## branch이동   
   새로 생성한 second branch 옮기기   
   ```s
      git checkout second
   ```   

   

1. # git 그래프로 확인하기
   ```s
      git log --graph
   ```   

1. # git master브랜치와 second브랜치 병합하기
   병합시 현재 위치한 브랜치에서 다른 브랜치를 가지고옵니다. master브랜치로 second브랜치를 병합하기 위해선 master브랜치로 먼저 이동해야됩니다.
   ```s
      git checkout master
      git merge second
   ```   
   
(github doc)[https://docs.github.com/en/get-started/quickstart/github-glossary#origin]