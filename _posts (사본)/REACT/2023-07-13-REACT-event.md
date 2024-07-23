---
layout: single
title: event사용
categories: REACT
tab: [useState]
---

1. # 선언 후 element에 할당
   ```javascript
      const App = () => {
         const handleClick = () => {
          alert("클릭했습니다.");
         }
         return  (
          <div>
            <button onClick={handleClick}>클릭하세요</button>
          </div>
         );
      };
   ```
1. # 익명함수로 바로 선언
   ```javascript
     const App = () => {
        return  (
          <div>
            <button onClick={() => { alert('클릭했습니다.') }
              }>클릭하세요</button>
          </div>
        )
      }
   ```
1. # 선언 후 할당 예제 : onChange이벤트에 함수를 할당
   ```javascript
      function App() {
         const handleChange = (event) =>{
           console.log(event.target.value); //value값을 가져온다.
         }

         return (
          <div className="App">
              <input onChange={handleChange} />
          </div>
         );
      }
   ```
1. # 익명함수로 바로 선언 예제
   ```javascript
      function App() {
        return (
          <div className="App">
              <input onChange={(event)=>{
                  console.log(event.target.value);
              }}/>;
          </div>
        );
      }

      export default App;
   ```
1. # 컴포넌트 내 이벤트처리
   ```javascript
      //App
      import React from 'react';
      import Greeting from './components/Greeting'

      function App() {
        return (
          <div className="App">
              <Greeting />
          </div>
        );
      }

      export default App;

      //Greeting component에서 이벤트 정의
      import React from "react";

      const Greeting = () = > {
          const handleClick = () => {
              alert("안녕하세요");
          }
          return <button onClick={handleClick}>클릭</button>;
      }

      export default Greeting;
   ```
1. # 이벤트와 state연동하기
   ```javascript
      import React, {useState} from 'react';

      function App() {
          const [inputValue, setInputValue] = useState("");

        return (
          <div className="App">
              <input onChange={(event) => {
                  setInputValue(event.target.value);
              }}/>
              <span>{inputValue}</span>
          </div>
        );
      }

      export default App;
   ```
1. # 한 개의 이벤트 핸들러를 여러 요소에 재사용하기
object 값을 변경할 때 object.key = "value" 또는 object["key"] = "value"처럼 변경할 수 있습니다. key대신 다른 변수를 사용해도 됩니다.
   ```javascript
   import React, {useState} from 'react';

   function App() {
       const [person, setPerson] = useState({
           name: "superMan",
           school: "초딩"
       });

       const handleChange = (event) => {
           const {name, value} = event.target;
           setPerson((current) => {
               const newPerson = { ...current };
               newPerson[name] = value;
               return newPerson;
           })
       }
     return (
       <div className="App">
           <input name="name" value={person.name} onChange={handleChange}/>
           <input name="school" value={person.school}  onChange={handleChange}/>
           <button onClick={() => {
               alert(`${person.name}은 ${person.school}이다.`);
           }}>클릭</button>
       </div>
     );
   }

   export default App;
   ```
