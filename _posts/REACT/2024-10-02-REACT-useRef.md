---
layout: single
title: export
categories: REACT
tab: 
---

1. # export
   ```javascript
      import Sub from './Sub'; //같은 폴더 위치의 default export
      import Top from './page/Top';  //page폴더의 위치의 default export
      import { num } from './Sub';  //named export
   ```

   default export는 컴포넌트당 1개만 가능합니다. 변수나 함수의 named export를 사용하는 경우 { }를 붙입니다.
   ```javascript
      import React from 'react';

      let num = 10;

      const Sub = () => {
         return (
            <div>
               
            </div>
         );
      };

      export {num} //추가적인 export 방법
      export default Sub; //default의 export는 1개밖에 못 함 
   ```
   num을 export할 때 { }를 사용하고 import 할 때도 { }를 사용합니다.   
