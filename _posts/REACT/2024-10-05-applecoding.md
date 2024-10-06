---
layout: single
title: applecoding 요약
categories: REACT
tab: [react]
---

1. # 요약
   -이미지 public 폴더-   
   배포할 때 압축하게 되는데 public 폴더에 있는 파일은 압축하지 않는다   

   public 폴더 안에 있는 이미지를 사용할 때 권장되는 방식   
   ```javascript
      <img src={process.env.PUBLIC_URL + 'img/logo.png'}>
   ```   
   서버에 배포 후 서버 경로에서 pbulic 이미지 경로를 참조하지 못 할 때 사용   

   -export-   
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