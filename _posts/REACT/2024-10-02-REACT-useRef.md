---
layout: single
title: useRef
categories: REACT
tab: 
---

1. # useRef

   1)전역 저장 요소로 사용   
   const ref = useRef(value);
   valuer값은 {current:value}형태로 저장됩니다. ref.current로 value값에 접근할 수 있습니다.   

   useState는 값이 저장될 때 랜더링이 되지만 useRef는 값이 저장되어도 랜더링 되지 않습니다. 일반 변수와 같은 역할을 합니다.   

   State의 변화 -> 렌더링 -> 컴포넌트 내부 변수들 초기화   
   Ref의 변화 -> No 렌더링 -> 변수들의 값이 유지됨   
   State의 변화 -> 렌더링 -> 그래도 Ref의 값은 유지됨   

   ```javascript
      const countRef = useRef(0);

      console.log(countRef); //출력 값 {current: 0}

      console.log(countRef.current); //출력 값 0
   ```

   => 자주 변경되는 변수를 useRef에 넣으면 성능에 이점이 있음.   

   *일반 변수와 차이점   
   useState로 랜더링을 시킬 경우 페이지를 다시 읽기 때문에 일반 변수는 기존 초기값으로 셋팅이 되지만 useRef 값은 랜더링이 되더라도 기존의 값을 그대로 유지한다는 차이점이 있습니다. 컴포넌트의 생명이 끝날 때까지 현재 값을 그대로 유지한 상태를 가집니다. useRef는 컴포넌트 생명주기와 함께한다는 관점에서 자바의 전역 변수와 유사한 점이 있습니다.   

   2)DOM 요소에 접근   
   DOM요소의 상태값을 변경할 수 있습니다. 예를 들어 로그인시 input box를 클릭하지 않아도 useRef를 사용하며 input box에 포커스를 줄 수 있습니다.   



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

JavaScript
import React, { useState, useEffect } from 'react';
import MyMap from './MyMap';

function App() {
  const [heatmapData, setHeatmapData] = useState([]);

  useEffect(() => {
    fetch('data.json')
      .then(response => response.json())
      .then(data => setHeatmapData(data));
  }, []);

  return (
    <div>
      {heatmapData.length > 0 && <MyMap heatmapData={heatmapData} />}
    </div>
  );
}