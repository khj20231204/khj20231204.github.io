---
layout: single
title: export
categories: REACT
tab: 
---


1. # 컴포넌트 사용시 { } 작성

   export를 할 때 default를 한 경우에만 import를 하는 곳에서 변수이름을 변경할 수 있습니다.   
   ```javascript
      -Bbb.jsx-

      import React from 'react';

      export const Ccc = () => {
         return(
            <h2>Ccc</h2>
         )
      }

      const Ddd = ( ) => {
         return(
            <h2>Ddd</h2>
         )
      }

      const Bbb = () => {
         return (
            <h2>Bbb</h2>
         );
      };

      export {Ddd}
      export default Bbb;
   ```   
   Ccc는 직접 export를 합니다.   
   Ddd는 export { } 로 export를 합니다.   
   Bbb만 default로 export를 합니다. default export는 1개만 가능합니다.   

   ```javascript
      -App.js-

      import './App.css';
      import { Ccc } from './Bbb';
      import { Ddd } from './Bbb';
      import BbbName from './Bbb'; //Bbb인 이름을 BbbName로 변경 가능

      function App() {
         return (
            <div className="App">
               <BbbName></BbbName>
               <Ccc></Ccc>
               <Ddd></Ddd>
            </div>
         );
      }

      export default App;
   ```
   Ccc와 Ddd 컴포넌트는 전부 Bbb컴포넌트 내부에 있고 default로 export가 안되기 때문에 `{ }`로 감싸줬고 이름변경이 안됩니다.   
   반면, Bbb자신의 컴포넌트로 export를 하는 경우 default가 가능하고 이 경우, 다른 이름으로 작명이 가능합니다.   
   Bbb 컴포넌트의 Ccc, Ddd 컴포넌트는 `{ }`로 둘러싸이고 다른 이름 안됨   
   Bbb 자신의 컴포넌트는 `{ }`가 없고 다른 이름 가능   

1. # 폴더 위치
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
