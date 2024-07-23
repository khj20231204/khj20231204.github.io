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