---
layout: single
title: useRef
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

1. # useRef
   useRef는 React에서 **참조(reference)**를 생성하고 관리하기 위한 Hook입니다. 쉽게 말해, 특정 값이나 DOM 요소를 가리키는 주소를 만들어주는 것이라고 생각할 수 있습니다.

   ref를 이용하여 포커스를 주는 예제
   ```javascript
      import { useRef, useEffect } from 'react';

         function MyComponent() {
         const inputRef = useRef(null);

         useEffect(() => {
            inputRef.current.focus(); // input 요소에 포커스 주기
         }, []);

         return (
            <div>
               <input ref={inputRef} />
            </div>
         );
      }
   ```

   ref를 이용하여 스타일을 바꾸는 예제
   ```javascript
      const UserRefEx = () => {
         let myRef = Array.from({length:5}).map(()=> createRef()); //ref를 동적으로 만들어주는 함수
         let list = [
            {id:1, name:'길동'},
            {id:2, name:'꺽정'}
         ]

         return(
            <>
               <button onClick={()=>{
                  myRef[0].current.style.backgroundColor = 'red';
               }}>색상변경</button>
               {list.map((v,i) => {
                  return (<h2 ref={myRef[i]}>{v.name}</h2>)
               })}
            </>
         );
      }
   ```

