---
layout: single
title: miniProject
categories: REACT(Lesson)
tag: []
author_profile: false
---

1. # miniProject

   App.js   
   ```js
      <Route index element={<MainPage/>}></Route> //index로 가장 먼저 보여주는 페이지
      <Route path="post-write" element={<PostWritePage/>}></Route>
      <Route path="post/:postid" element={<PostViewPage/>}></Route>
   ```   

   MainPage에 "글 작성하기"버튼과 "PostList"가 있는데 PostList가 화면에 목록을 뿌려준다
   MainPage -> PostList -> PostListItem   

   MainPage에서 json파일을 data란 이름으로 가져와서 사용가능, import하면 가능
   ```cs
      import data from '../../data.json';
   ```
