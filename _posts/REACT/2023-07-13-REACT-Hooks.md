---
layout: single
title: Hook
categories: REACT
tab: [Effect Hook]
---

1. # Effect Hook 1
   ```javascript
      import React, {useState, useEffect} from 'react';

      function App() {
          const [inputValue, setInputValue] = useState("");

          useEffect(()=>{
              console.log(inputValue);
          }, [inputValue])

        return (
          <div className="App">
              <input value={inputValue} onChange={(event)=>{
                  setInputValue(event.target.value);
              }} />
          </div>
        );
      }

      export default App;
   ```
   state값이 변할 때마다 effecHook이 작동합니다.
1. # Effect Hook 2
   컴포넌트가 생성되고 소멸될 때 effectHook이 작동합니다.
   ```javascript
      //App
      import React, {useState} from 'react';
      import Greeting from './components/Greeting';

      function App() {
          const [isCreated, setIsCreated] = useState(false);
        return (
          <div className="App">
              <button onClick={()=>{
                  setIsCreated((current)=>{
                      return !current;
                  })
              }}>컴포넌트 생성/제거</button>
              {isCreated && <Greeting />}
          </div>
        );
      }
      export default App;

      //Greeting
      import React, {useEffect} from "react";

      const Greeting = () => {
         useEffect(() => {
              console.log("컴포넌트 생성");
              return () => {
                  console.log("컴포넌트 소멸");
              }
          }, []); //[] 빈칸 대괄호는 컴포넌트의 생성과 소멸시 useEffect가 실행됩니다.

          return <h1>안녕하세요.</h1>;
      }
      export default Greeting;
   ```
   useEffect 훅의 두 번째 매개변수로 빈 배열([])이 전달되었기 때문에 콜백 함수는 컴포넌트가 생성될 때 한 번만 호출되고, 컴포넌트가 소멸될 때 한 번만 호출되는 반환 함수를 반환합니다.   
   따라서, 위의 코드에서는 “컴포넌트 생성”이라는 메시지가 컴포넌트가 생성될 때 콘솔에 출력되고, 이후 컴포넌트가 소멸될 때 “컴포넌트 소멸”이라는 메시지가 콘솔에 출력됩니다. 이 경우, 컴포넌트가 생성되자마자 소멸되므로 실제로 컴포넌트가 화면에 렌더링되지는 않을 것입니다.

   submit이 일어나면 페이지 새로고침이 된다 이걸 방지하기 위해서 event.preventDefault()를 사용한다.