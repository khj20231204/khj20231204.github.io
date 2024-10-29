---
layout: single
title: 이슈 정리
categories: PROJECT
tag: []
author_profile: false
---   

1. # 부트스트랩의 href를 link로 변경

1. # 자바스크립트 사용하기

   ```
      Cannot read properties of null (reading 'addEventListener')
      TypeError: Cannot read properties of null (reading 'addEventListener')
         at __webpack_modules__../src/LoginForm.js.window.onload (http://localhost:3000/static/js/bundle.js:214:13)
   ```

   css의 class를 className으로 변경   
   css앞에 전부 loginformjs 붙이기    
   const container = document.querySelector(".loginformjs .container");
   "container" 값이 헤더의 container값을 가져왔다   

   

   window.onload 사용
   ```
      window.onload = function(){

      const signUpBtn = document.getElementById("signUp");
      const signInBtn = document.getElementById("signIn");
      const container = document.querySelector(".container");

         signUpBtn.addEventListener("click", () => {
            alert("df");
         container.classList.add("right-panel-active");
         
         });
         
         signInBtn.addEventListener("click", () => {
         alert("geg");
         container.classList.remove("right-panel-active");
         });
      } 
   ```

   script async로 삽입
   ```
      <div id="root"></div>
    <!-- js파일 삽입-->
    <!-- <script async src="assets/js/LoginForm.js"></script> -->

   ```

   이벤트는 3가지의 중심 요소가 존재한다.  어떤 이벤트를 발생시킬 것인지의 이벤트event, 이벤트가 발생하면 실행되게 할 함수 event handler, 그리고 이벤트와 함수를 연결하는 addEventListener가 있다 addEventListener(event, handler, useCapture); addEventListener는 이벤트와 핸들러를 연결짓는 함수이다
   *useCapture: (선택 사항) 이벤트 버블링과 캡처링 중 어떤 방식으로 이벤트를 처리할지 결정하는 boolean 값