---
layout: single
title: Window에서 실행
categories: JekyllBlog
tag: []
author_profile: false
---

1. # ruby 설치
   <a href="https://rubyinstaller.org/downloads">https://rubyinstaller.org/downloads</a>   
   여기서 WITH DEVKIT 3.2.4-1을 다운 받습니다.   

   <img src="../../imgs/JekyllBlog/win_install_1.png" style="border:3px solid black;border-radius:9px;width:800px">   
   조건 2개를 모두 선택합니다.   

1. # jekyll과 번들러 설치

   2. jekyll번들러 설치
   ```s
      gem install jekyll bundler
   ```   
   <img src="../../imgs/JekyllBlog/win_install_2.png" style="border:3px solid black;border-radius:9px;width:800px">   

   2. gem 번들러 설치
   ```s
      gem install bundler
   ```
   <img src="../../imgs/JekyllBlog/win_install_3.png" style="border:3px solid black;border-radius:9px;width:800px">   

   2. powershell로 이동
   <img src="../../imgs/JekyllBlog/win_install_4.png" style="border:3px solid black;border-radius:9px;width:800px">   
   블로그 디렉토리에서 powershell로 이동 후   

   2. 번들 설치   
   <img src="../../imgs/JekyllBlog/win_install_5.png" style="border:3px solid black;border-radius:9px;width:800px">   
   ```s
      bundle install
   ```

   2. 서버 실행   
   ```s
      bundle exec jekyll serve
      또는
      jekyll s
   ```

   2. 블로그 연결
   http://localhost:4000/



