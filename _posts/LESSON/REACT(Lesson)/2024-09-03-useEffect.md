---
layout: single
title: useEffect
categories: REACT(Lesson)
tag: []
author_profile: false
---

1. # useEffect
   useEffect는 리액트 컴포넌트가 렌더링될 때마다 특정 작업이 수행하도록 설정 할 수 있는 훅(hooks)입니다.   
   
   1.useEffect는 리액트 컴포넌트가 렌더링될 때마다 특정 작업이 수행하도록 설정 할 수 있는 훅(hooks)입니다.   
   2.컴포넌트가 마운트 됐을 때(처음 나타났을 때), 언마운트 됐을 때(사라 질때) 업데이트 될 때(특정 props가 바뀔 때) 처리할 수 있는 훅입니다.   

   useEffect ( 이펙트 함수, 의존성 배열 )    
   1.첫 번째 파라미터는 이펙트 함수가 들어가고, 두 번째 파라미터는 의존성 배열이 들어간다. 이때 배열안에 들어 있는 변수 중에서 하나라도 값이 변경
   되었을때 이펙트 함수가 실행된다.   
   2.이펙트 함수는 처음 컴포넌트가 렌드링된 이후와 업데이트로 인한 재렌더링 이후에 실행된다.   
   3.이펙트 함수를 마운트와 언마운트시에 단 한번만 실행되게 하고 싶으면, 의존성 배열에 빈 배열( [ ] )을 넣으면 된다.   
   4.의존성 배열은 생략할 수도 있는데, 생략하게 되면 컴포넌트가 업데이트 될 때 마다 호출된다.   

   ```cs
      useEffect ( () => {
      //1.컴포넌트가 마운트 된 이후, 의존성 배열에 있는 변수들 중 하나라도 값이 변경 되었을때 실행됨
      //2.의존성 배열에 빈 배열([])을 넣으면, 마운트와 언마운트시에 단 한번씩만 실행됨
      //3.의존성 배열 생략 시 컴포넌트 업데이트 시마다 실행됨
      } , [의존성 변수1, 변수2, …] );
   ```   

   1)렌더링 될 때마다 title변경
   ```javascript
      import React,{useState, useEffect} from 'react';

      const Counter2 = () => {

         const [count, setCount] = useState(0);

         //useEffect는 리액트 컴포넌트가 랜더링 될 때마다 특정 작업이 수행되도록
         //설정할 수 있는 훅
         useEffect(() => {
            document.title = count + '번 클릭';
            console.log(count + '번 클릭');
         });

         return (
            <div>
               <p>총 {count}번 클릭 했습니다.</p>
               <button onClick={() => setCount(count+1)}>클릭</button>
            </div>
         );
      }

      export default Counter2;
   ```

   2)렌더링 되는 경우   
   첫 렌더링에 2번 뜸

   렌더링 될때 마다 리로딩 방지

   ```javascript
      const Info2 = () => {

         const [name, setName] = useState('');
         const [nickname, setNickname] = useState('');

         const onChangeName = (e) => {
            setName(e.target.value);
         }

         const onChangeNickname = (e) => {
            setNickname(e.target.value);
         }

         useEffect(() => {
            console.log('렌더링이 완료 되었습니다.');
            console.log({name, nickname});
         }, []);
         //하단 가장 뒤에 [] 비어있는 배열을 추가하면 useEffect가 처음 렌더링될 때 한번만 실행됨

         return (
            <div>
               <div>
                  <input onChange={onChangeName}/>
                  <input onChange={onChangeNickname}/>
               </div>
               <div>이름 : {name}</div>
               <div>닉네임 : {nickname}</div>
            </div>
         );
      };
   ```

   3)state가 변경될 때만 useEffect실행   
   ```javascript
      function App() {

         const [data, setData] = useState(0);
         const [search, setSearch] = useState(0);

         let downLoad = () => {
            setData(5);
         }

         useEffect(() => {
            console.log("useEffect 실행됨");
            downLoad();
         },[search])  //setSearch(2)가 실행되면 useEffect 1번 실행됨, 이후로는 search값이 2로 변경이 없기 때문에 실행 안됨

         return (
            <div>
               <button onClick={() => {
                  setSearch(2);
               }}>검색하기</button>
               <h2>데이터 : {data}</h2>
               <button onClick={() => {
                  setData(data+1);
               }}>더하기</button>
            </div>
         );
      }

      export default App;
   ```

1. # React에서 렌더링되는 경우
   React 컴포넌트는 특정 조건이 만족될 때마다 다시 렌더링되어 화면에 반영됩니다. 이러한 렌더링 과정은 React 애플리케이션의 핵심 동작 중 하나이며, UI를 동적으로 업데이트하는 데 필수적입니다.   

   React 컴포넌트가 렌더링되는 주요 경우는 다음과 같습니다   

   1.최초 렌더링   
   컴포넌트가 처음 생성되고 화면에 나타날 때 렌더링됩니다.   
   초기 props와 state 값을 기반으로 UI가 구성됩니다.   

   2.props 변경   
   부모 컴포넌트에서 자식 컴포넌트로 전달되는 props 값이 변경될 때 자식 컴포넌트가 렌더링됩니다.   
   props는 컴포넌트의 입력값과 같으며, 이 값이 변경되면 컴포넌트는 새로운 props를 반영하여 UI를 업데이트합니다.   

   3.state 변경   
   컴포넌트 내부의 state 값이 변경될 때 컴포넌트가 렌더링됩니다.
   state는 컴포넌트의 내부 상태를 나타내며, 이 값이 변경되면 컴포넌트는 새로운 state를 반영하여 UI를 업데이트합니다.   

   4.부모 컴포넌트 렌더링   
   부모 컴포넌트가 렌더링될 때, 자식 컴포넌트도 함께 렌더링될 수 있습니다.
   부모 컴포넌트의 렌더링은 자식 컴포넌트의 props 변경을 유발할 수 있으며, 이는 자식 컴포넌트의 렌더링을 트리거합니다.   




