---
layout: single
title: Custom Hook 
categories: REACT
tab: 
---

1. # Hook과 Component비교
   컴포넌트는 클래스 단위의 큰 개념, 훅은 함수 단위의 작은 개념   

   컴포넌트는 `<Component>`로 전체를 사용하지만   
   훅은 `let [myHook] = MyHook`으로 변수를 지정해서 사용   

1. # Hooks 만들기
   MyHook에 있는 state와 함수를 리턴해주면 import한 곳에서 MyHook 내부에 있는 state와 함수를 가져다 사용할 수 있습니다.   

   컴포넌트가 아니기 때문에 함수명(파일명 역시)은 소문자로 합니다.   

   -myHooks.js-   
   ```javascript
      import { useState } from 'react';

      export const myHooks = () => { //함수(파일명와 일치)를 export

         let [hart, setHart] = useState(0); //state선언

         let myhooksFunc = () => { //함수 선언
            setHart(hart+1)
         }

         return [hart, myhooksFunc]; //state와 함수를 리턴
      };
   ```

   myHooks를 export하고 hart state와 myhooksFunc인 함수를 리턴하면,   
   myHooks를 import한 곳에서 리턴한 state와 함수를 사용할 수 있습니다.   

   -App.js(myHooks를 사용하는 곳)-   
   ```javascript
      import { myHooks } from './hooks/myHooks'; //myHooks를 import

      function App() {

      let [hart, myhooksFunc] = myHooks();
      /*
      myHooks는 함수기 때문에 ()가 붙는다
      리턴을 배열로 했기 때문에 구조분해할당도 배열로 한다
      */

      return (
         <div className="App">
            //myHooks의 함수와 state 사용
            <span onClick={myhooksFunc} style={{cursor:'pointer'}}>❤️{hart}</span>
         </div>
      );
      }

      export default App;
   ```