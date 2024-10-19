---
layout: single
title: delete시 where조건 없애기
categories: MYSQL
tag: []
author_profile: false
---
 
1. # Safe Update 설정

   delete를 할 때 where 조건이 없으면 실행이 되지 않는 경우가 있습니다. 전체 데이터가 삭제되는 것을 막기 위한 옵션이 선택되어 있기 때문입니다.

    <img src="../../imgs/mysql/safe_updates.png" style="border:3px solid black;border-radius:9px;width:800px">  

    해당 옵션에서 빨간색 표에 마크를 없애줍니다.   