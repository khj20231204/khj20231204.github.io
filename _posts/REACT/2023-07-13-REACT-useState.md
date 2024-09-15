---
layout: single
title: useState
categories: REACT
tab: [useState]
---

# useState 사용 예제
   ```javascript
      function App() {
         const [person, setPerson] = useState({
               name: "김민수",
               count: 0
         });
         return (
         <div className="App">
               <button onClick={()=>{
                  setPerson((current)=>{
                     const newPerson = {...current};
                     newPerson.count = newPerson.count  + 1;
                     return newPerson;
                  })
               }}>클릭</button>
               <span>{person.name}님이 버튼을 {person.count}회 클릭하였습니다.</span>
         </div>
         );
      }
   ```
   버튼을 클릭할 때마다 1씩 증가

   ```javascript
      //App
      import React, {useState} from 'react';
      import Greeting from "./components/Greeting"

      function App() {
      const [username, setUsername] = useState("");
         return (
            <div className="App">
               <input value={username} onChange={(event) => {
                  setUsername(event.target.value);
                  }} />  
                  <Greeting username={username} />
            </div>
         );
      }

      //Greeting Component
      import React from "react";

      const Greeting = ({username})=>{
         return <h1>{username}님 안녕하세요</h1>
      };
      export default Greeting;
   ```
   component를 사용하여 username 호출

1. # 배열에 값 입력시 제대로 동작 안함
   ```javascript
      const [subject, setSubject] = useState(['가을남자','정장','헤어스타일']);

      return (
         <div className="App">
            <h4 className="blogTitle"> React Blog</h4>
               <div>
                  <h5 className="subjectTitle">{subject[0]}</h5>
               </div>
               
               <button type="button" onClick={() => {
               
                  /** 제대로 동작하지 않음 **/                  
                  /* 얕은 복사 */
                  let copy = subject;
                  /* useState의 특징 */
                  copy[0] = "아이쿠 그냥 추천";
                  setSubject(copy);

                  /** 제대로 동작 **/
                  const newSubject = [...subject];
                  newSubject[0] = "아이쿠 그냥 추천";
                  setSubject(newSubject);

               }}>타이틀 변경</button>
         </div>
      )
   ```   
   __얕은 복사__   
   let copy = subject; 는 배열 subject를 새로운 변수 copy에 할당하는 것처럼 보이지만, 실제로는 두 변수가 같은 배열 객체를 참조하게 됩니다. 즉, copy를 수정하면 subject도 함께 수정되는 얕은 복사가 발생합니다.   

   __useState의 특징__   
   useState는 상태 변경 시 <span style="color:red">새로운 값을 만들어서</span> 상태를 업데이트해야 합니다. 기존 상태를 직접 수정하면 React는 변화를 감지하지 못하고 렌더링되지 않습니다.   