---
layout: single
title: VScode Spaces 바뀌는 않게 설정
categories: etc
tag: []
---

1. # Spaces설정
   VScode가 처음 로딩하면 현재 상태에 따라 Spaces간격을 2나 3으로 변경합니다. 변경되는 것을 막고 계속 유지하는 방법입니다.   

   ctrl+shift+p -> user settings json(user settings을 json파일로 설정)    

   ```javascript
      "editor.tabSize": 3, //tab사이즈 설정
      "editor.detectIndentation": false,  //자동 감지 끄기
   ```   
   위에 코드를 입력합니다.   