---
layout: single
title: metacoding 요약
categories: REACT
tab: [react]
---

1. # 실행 순서
   npm start →   
   index.js : index.html파일의 root를 찾는다   
   ```javascript
      const root = ReactDOM.createRoot(document.getElementById('root')); //index.html파일에서 id = root를 찾는다
      root.render(  //index.html의 root에 밑에 부분을 랜더링
         <React.StrictMode>
            <App />
         </React.StrictMode>
      );
   ```
   → App.js   

   __index.js에서 index.html에 App.js를 랜더링__   

   *React : 엔진이다. 데이터변경을 감지해서 UI를 그려주는   

   __조건부__   
   ```javascript
      <h2> {a === 10 ? 10입니다} </h2>
   ```