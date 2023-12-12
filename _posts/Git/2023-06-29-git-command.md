---
layout: single
title: git 명령어
categories: Git
tag: [git]
---

1. ## add한 파일 취소하기
   reset명령어를 이용하면 됩니다. reset명령은 add를 해서 staging area에 있는 파일을 다시 working directory로 옮기는 역할을 합니다.
   ```
      git reset README.md
   ```
1. ## branch 목록확인
   ```
      git branch 
   ```
1. ## second란 이름의 branch 생성
   ```
      git branch second
   ```
1. ## 새로 생성한 second branch 옮기기
   ```
      git checkout second
   ```
1. ## git 그래프로 확인하기
   ```
      git log --graph
   ```
1. ## git master브랜치와 second브랜치 병합하기
   병합시 현재 위치한 브랜치에서 다른 브랜치를 가지고옵니다. master브랜치로 second브랜치를 병합하기 위해선 master브랜치로 먼저 이동해야됩니다.
   ```
      git checkout master
      git merge second
   ```
