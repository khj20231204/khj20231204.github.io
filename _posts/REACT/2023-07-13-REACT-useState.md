---
layout: single
title: useState
categories: REACT
tab: [useState]
---

1. # useState
   <a href="../LESSON/REACT(Lesson)/2024-09-03-useSate.md">다른 설명</a>

   ```javascript
      let [number, setNumber] = useState(0);

      setNumber(number++) //(X)
      setNumber(number+1) //(O)
   ```  
   number++ 인 경우 number = number+1 이기 때문에 결과 값이 다시 number에 입력됩니다. 그렇기 때문에 number에 1을 증가시킨 number+1을 입력해야 합니다.   

   위치 값으로 변수, 변수설정이 결정됩니다.
   let [a, b, c] = useState('')라고 하면 b가 setA의 역할이 됩니다. c는 undefined가 됩니다.   
   ```javascript
      const Aaa = () => {
         let [a, b,c] = useState('');

         let changeA = () => {
            b('a값 변경')
         }

         return (
            <div>
               <div onClick={changeA}>클릭!</div>
               {console.log({a})} //""
               {console.log({b})} //f()
               {console.log({c})} //undefined
            </div>
         );
      };

      export default Aaa;
   ```

1. # useState 사용 예제
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

1. # 배열로 초기화
   ```javascript
      let sample = [
       {id:1, name:"A"},
       {id:2, name:"B"},
       {id:3, name:"C"},
       {id:4, name:"D"},
     ];

      let [users, setUsers] = useState(sample) // --- 1)
      let [users, setUsers] = useState([sample]) // --- 2)
   ```
   1)let [users, setUsers] = useState(sample)   
   여기서는 sample 배열이 직접 상태의 초기값으로 설정됩니다. 따라서 users의 초기값은 sample 배열의 내용, 즉 [{id:1, name:"A"}, {id:2, name:"B"}, {id:3, name:"C"}, {id:4, name:"D"}]입니다.   

   2)let [users, setUsers] = useState([sample])   
   이 경우 sample 배열이 새로운 배열로 감싸져 있습니다. 따라서 users의 초기값은 [sample]이 되며, 결과적으로 users는 배열의 배열이 됩니다. 즉, users의 값은 [[{id:1, name:"A"}, {id:2, name:"B"}, {id:3, name:"C"}, {id:4, name:"D"}]]가 됩니다.   


1. # 배열에 값 입력시 랜더링 안함 - 1
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
                  //subject의 원래 주소값과 copy의 원래 주소값이 같아 실제로는 변경된 것이 없다.
                  let copy = subject;

                  /* useState의 특징 적용*/
                  copy[0] = "아이쿠 그냥 추천";

                  /* copy[0]의 주소값이 변경되었지 copy의 주소값이 변경된 건 아니다*/
                  setSubject(copy);

                  /** 제대로 동작 **/
                  //[...obj] 이 문법을 사용하면  화살표가 새로 생긴다.
                  //따라서 newSubject와 subject 주소가 다른다.   
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

1. # 배열에 값 입력시 랜더링 안함 - 2
   ```javascript
      let sample = [
         {id:1, name:"A"},
         {id:2, name:"B"},
         {id:3, name:"C"},
         {id:4, name:"D"},
      ];

      //1)동작 함
      let [users, setUsers] = useState([]) //초기값 설정 안 함

      let download = () => {
         setUsers(sample) 
      }

      //2)동작 안함
      let [users, setUsers] = useState(sample) //초기값을 sample로 입력

      let download = () => {
         setUsers(sample)  //초기값과 같은 reference
      }

      //3)동작 함
      let [users, setUsers] = useState(sample) //초기값을 sample로 설정하지만

      let download = () => {
         setUsers([...sample])  //spread 연산자를 사용함, spread연산자를 사용할 땐 [ ] 입력해야함
      }

      //4)
      let [users, setUsers] = useState(sample) //초기값을 sample로 입력

      let download = () => {
         sample.push({id:7, name:'kk'}) //비록 push를 넣어서 sample값을 변경했지만 deep copy아니기 때문에 랜더링 안됨
         setUsers(sample)  //초기값과 같은 reference
      }

      //5)
      let [users, setUsers] = useState(sample) //초기값을 sample로 입력

      let download = () => {
         let sample2 = sample.concat({id:7, name:'kk'}) //concat으로 깊은 복사를 하게되면 랜더링 됨
         setUsers(sample2)  //concat으로 인해 초기값과 다른 reference를 가지게 됨
      }
   ```

1. # 자식이 부모의 state를 가져다쓰고 싶을 때는 props
   부모 -> 자식 state 전송하는 법   

   1.부모:<자식컴포넌트 작명={state이름}>   
   ```javascript
      const Parent = () => {
         return(
            <div>
               <Child color={'skyblue'} />
            </div>
         )
      }
   ```   

   2.자식:props파라미터 등록 후 props.작명 사용   
   ```javascript
      const Child = (props) => {
         return(
            <div>
               <p>{props.color}</p> // 배열인 경우 모든 원소값들 출력
               <p>{props[1]. color}</p>  //props배열의 1번째 인덱스 값 가져오기
            </div>
         )
      }
   ```   

   props 전송은 부모 -> 자식만 가능   

   자식이 부모에게 전달하거나 형제끼리 전달하는 거 모두 불가능   

   <span style="color:red">*state 만드는 곳은  state를 사용하는 컴포넌트들 중 최상위 컴포넌트에 선언.</span>   
   왜? state는 props로 부모->자식으로만 전달되기 때문.


   