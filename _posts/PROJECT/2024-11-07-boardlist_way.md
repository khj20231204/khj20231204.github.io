---
layout: single
title: boardlist화면 해석
categories: PROJECT
tag: []
author_profile: false
---   

1. # boardlist부분 해석
   
   메인 -> 게시판 클릭 -> 클라이언트 : useEffet에서 axios 실행 -> 서버 : 스프링 Controller -> Board.jsx🎮   

   
   1️⃣axios의 비동기 방식으로 Controller에 값 전달 후 전달 받기   
   ```javascript
       if(page === '' || page === null)
         page = 1;


       response = await boardapi.list(page, board);
         }catch(error){
         console.log(error);
      }

      setPage(response.data.currentPage);
      setTotalPage(response.data.pp.totalPage)
      setBoardList([...response.data.list]); //흩뿌리기
   ``` 
   2️⃣
   3️⃣
   4️⃣
   6️⃣
   5️⃣
   7️⃣
   8️⃣9️⃣🔟