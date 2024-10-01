---
layout: single
title: Hooks
categories: REACT
tab: [Effect Hook]
---

1. # 훅의 종류
   __useState: 상태 관리__   
   컴포넌트 내부에서 데이터를 저장하고 변경할 수 있도록 합니다.   
   예: 버튼 클릭 시 카운트 증가   

   __useEffect: 부가 효과__   
   컴포넌트가 화면에 나타나거나 업데이트될 때 특정 작업을 수행합니다.   
   예: 데이터 Fetch, 타이머 설정, DOM 조작   
   
   __useContext: 컨텍스트 API 사용__   
   컴포넌트 트리 전체에 데이터를 전달하고 공유합니다.   
   예: 테마 변경, 로그인 상태 관리   
   
   __useReducer: 복잡한 상태 관리__   
   상태 업데이트 로직을 함수로 분리하여 관리합니다.   
   예: 여러 개의 상태를 가진 복잡한 폼   
   
   __useMemo: 값 메모이제이션__   
   비싼 연산 결과를 캐싱하여 불필요한 재연산을 방지합니다.   
   예: 복잡한 계산, 큰 배열 필터링   
   
   __useCallback: 콜백 함수 메모이제이션__   
   자주 변경되지 않는 콜백 함수를 메모이제이션하여 성능을 향상시킵니다.   
   예: 최적화된 이벤트 핸들러   
   
   __useRef: DOM 노드 참조__   
   DOM 노드에 대한 참조를 유지합니다.   
   예: 포커스 설정, 직접적인 DOM 조작   
   
   __custom hooks: 커스텀 훅 생성__   
   특정 로직을 재사용 가능한 훅으로 만들어 코드를 모듈화합니다.
   예: 커스텀 폼 훅, 데이터 Fetch 훅

1. # Hooks 사용 위치
   ```javascript
      import useState from 'react';

      //const [number, setNumber] = useState();  //---- 1)error발생

      function App() {

         const [number, setNumber] = useState();  //---- 2)사용할 위치

         return (
            <div>
               //const [number, setNumber] = useState();  //---- 3)error 발생
            </div>
         );
      }

      export default App;
   ```
   변수와 함수는 1),2)에서 사용가능 하지만 hook는 2) 위치에서만 사용가능합니다.   

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