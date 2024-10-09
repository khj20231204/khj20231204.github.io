---
layout: single
title: applecoding 요약
categories: REACT
tab: [react]
---

1. # 요약
   __-이미지 public 폴더-__   
   배포할 때 압축하게 되는데 public 폴더에 있는 파일은 압축하지 않는다   

   public 폴더 안에 있는 이미지를 사용할 때 권장되는 방식   
   ```javascript
      <img src={process.env.PUBLIC_URL + 'img/logo.png'}>
   ```   
   서버에 배포 후 서버 경로에서 pbulic 이미지 경로를 참조하지 못 할 때 사용   

   __-이미지 출력 방법-__   
   __1)외부css의 background-image : url()__   
   ```cs
      background-image: url('./imgs/main.jpg');
   ```

   1-1)src 폴더   
   ```cs
      background-image: url('./imgs/main.jpg');
   ```

   1-2)public 폴더 : X(적용 안됨)   

   <br>

   __2)요소 태그에서 바로 출력__   
   ```cs
      <img src={bg} width="100px"></img>
      <div className="main-bg" style={{ backgroundImage : 'url(' + bg + ')' }}></div>
   ```   

   2-1)src 폴더 : import를 해야된다    
   ```cs
      import bg from './imgs/main.jpg' 
   ```   

   2-2)public 폴더 : process.env.PUBLIC_URL   
   ```cs
      <img src={process.env.PUBLIC_URL + bg} width={300}/>
   ```

   __-export-__   
   __export를 여러개 하려면 export {변수1, 변수2}__   
   __import를 여러개 하려면 {변수1, 변수2} from '경로'__   

   data.js를 App.js에서 사용할 때   

   data.js
   ```javascript
      let a = 10;
      let b = 100;

      export {a,b};
   ```

   App.js   
   ```javascript
      import {a,b} from './data.js'
   ```

   data.js json으로 변경 후   
   ```javascript
      let data = [
         {
            id : 0,
            title : "White and Black",
            content : "Born in France",
            price : 120000
         },

         {
            id : 1,
            title : "Red Knit",
            content : "Born in Seoul",
            price : 110000
         },

         {
            id : 2,
            title : "Grey Yordan",
            content : "Born in the States",
            price : 130000
         }
      ] 

      export default data;
   ```

   useState에 넣을 때는 바로 data를 넣는다.   
   ```javascript
      let [shoes] = useState(data);

      shoes[0].title; //"White and Black"
      shoes[1].id;  //1
   ```

   __-Router-__   
   ```javascript
      <BrowserRouter>
         <Routes>
            <Route path="/" element={<Main/>}></Route>
            <Route path="/detail" element={<Details/>}></Route>
         </Routes>
      </BrowserRouter>
   ```

   __useNavigate사용__   
   ```javascript
      import { useNavigate } from 'react-router-dom';

      <button onClick={ navigate('/detail') }>detail</button>
      <button onClick={ () => navigate(1) }>뒤로</button> //앞으로 한페이지 이동
      <button onClick={ () => navigate(-1) }>뒤로</button>  //뒤로 한페이지 이동
   ```

   __404페이지__   
   ```javascript
      <Route path="*" element={<h1>없는 페이지 입니다.</h1>}></Route>
   ```

   __netsted Routes__   
   페이지 내에 페이지 출력   

   App.js   
   ```javascript
      <Route path="/detail" element={<Details/>}>
         <Route path="page1" element={<Page1/>}/>
         <Route path="page2" element={<Page2/>}/>
      </Route>
   ```

   detail페이지에 <Outlet>을 설정한 곳에   
   /detail/page1 => page1이 detail페이지의 <Outlet>에 출력   
   /detail/page2 => page2가 detail페이지의 <Outlet>에 출력   
   
   detail.js   
   ```javascript
      <div className="col-md-6">
         <p>상품설명</p>
         <p>120000원</p>
         <Outlet/>  //<-- 여기에 page1 또는 page2가 출력
      </div>
   ```
