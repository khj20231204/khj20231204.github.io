---
layout: single
title: Component
categories: REACT(Lesson)
tag: []
author_profile: false
---

1. # Component
   1.리액트를 사용하여 애플리케이션의 인터페이스를 설계할때 사용자가 볼 수 있는 요소는 여러가지 컴포넌트로 구성됩니다.   

   2.컴포넌트를 선언하는 방식은 클래스형 컴포넌트와 함수형 컴포넌트가 있습니다.   

   3.클래스형 컴포넌트는 state 기능 및 라이프사이클 API를 사용할 수 있습니다.   

   4.함수형 컴포넌트의 단점은 state와 라이프사이클 API를 사용할 수 없었지만, 리액트 v16.8 이후에 훅(Hooks)이라는 기능이 도입 되면서 해결 되었습니다.   

   5.리액트 공식 매뉴얼에서는 함수형 컴포넌트와 Hooks을 사용하도록 권장하고 있습니다.   

   6.컴포넌트의 첫 글자는 항상 대문자로 시작 해야합니다. 컴포넌트를 소문자로 시작하면 DOM 태그로 처리합니다.   

   7.컴포넌트를 이용해서 UI를 재사용 가능한 개별적인 여러 조각으로 나누고, 각 조각을 개별적으로 나누어 코딩합니다.   

   8.자식 컴포넌트에게 값을 전달할때 props를 사용할 수 있습니다.   

1. # 클래스형 컴퍼넌트

   ```javascript
      import react, {Component} from "react";

      class App1 extends Component{
         render(){
            const name = '클래스형 컴포넌트';
            return <div className="react">{name}</div>
         }
      }

      export default App1;
   ```   
   상단에 react와 {Component}를 추가해줘야 합니다.   
   그리고 Component를 상속받아야 하고 render   

1. # 함수형 컴퍼넌트   

   ```javascript
      import React from "react";
      import './App.css';

      //function App2(){
      const App2 = () => {      //ES6문법으로 함수 생성
         const name = '함수형 컴포넌트';
         return <div className="react">{name}</div>
      }

      export default App2;
   ```   

1. # props로 값 받기
   1.props는 프로퍼티(properties)의 줄임말입니다.   
   2.props는 부모 컴포넌트에서 자식 컴포넌트에게 데이터를 전달할 때 사용합니다.   
   3.props를 전달받은 자식 컴포넌트에서는 데이터를 수정할 수 없습니다.   

   index.js -> App.js(부모) -> MyComponent3.js(자식)   
   
   <br>
   index.js
   ```javascript
      import React from 'react';
      import ReactDOM from 'react-dom/client';
      import './index.css';
      import App from './App';      //App 등록
      import reportWebVitals from './reportWebVitals';

      const root = ReactDOM.createRoot(document.getElementById('root'));
      root.render(
      <React.StrictMode>
         <App />              //App 호출
      </React.StrictMode>
      );
   ```   
   <br>
   App.js
   ```javascript
      import MyComponent from './component/MyComponent.js'; //부모에서 자식 컴포넌트를 import

      const App = () => {
         <div>
            return <MyComponent name="React">리액트</MyComponent> {/* 값 전달 방식 */}
         </div>
      }

      export default App;
   ```
   <br>
   MyComponent.js
   ```javascript
      const MyComponent = (props) => {

         return (
            <div>
               <h1>안녕하세요</h1>
               <h3>내이름은 {props.name}이다</h3> <br/> {/* react 출력 */}
                  children 값은 {props.children} 이다.   {/* 리액트 출력 */}
            </div>
         );
      }

      export default MyComponent;
   ```   
   props객체를 매개변수를 받아서 `.`연산자를 통해 객체의 프로퍼티에 접근합니다.   
   name은 부모에서 받은 변수명이 되기 때문에 다른 이름으로 변경이 됩니다.   
   하지만, children은 내장 API이기 때문에 변경을 못 하면 텍스트 값을 가져옵니다.   
   여기선 '리액트'란 문구가 나타납니다.   

1. # 매개변수로 값 받기

   ```javascript
      //App.js
      return <MyComponent name="React" num={34}>리액트</MyComponent5>

      //MyComponent.js
      const MyComponent5 = ({name, children, num}) => {
         return (
            <div>
               <h1>안녕!</h1><br/>
               <h2>나의 이름은 {name}이다.</h2><br/>
               <h3>나의 children은 {children}이다.</h3><br/>
               <h4>내가 좋아하는 숫자는 {num}이다.</h4><br/>
            </div>
         );
      }
      
      export default MyComponent;
   ```   
   `<MyComponent name="React" num={34}>` 문자를 넘겨줄 때는 `"` 나 `'` 를 사용해야하고 숫자를 넘겨줄 때는 `{ }`를 사용해야 합니다.   
   name과 num은 부모 컴포넌트 App.js에서 넘겨준 변수 값이며 children은 JSX의 내장API입니다.

1. # props로 값을 받아 비구조화 할당

   ```javascript
      //App.js
      return <MyComponent name="React" num={34}>리액트2</MyComponent>
      
      //MyComponent6.js
      const MyComponent = (props) => {
         const {name, children, num} = props;   //비구조화 할당

         return (
            <div>
               <h1>안녕!</h1><br/>
               <h2>나의 이름은 {name}이다.</h2><br/>
               <h3>나의 children은 {children}이다.</h3><br/>
               <h4>내가 좋아하는 숫자는 {num}이다.</h4><br/>
            </div>
         );
      }

      export default MyComponent;
   ```   

1. # 컴포넌트 나누기
   Header.js / Main.js / Footer.js 로 3개의 컴포넌트를 나눠서 App.js 에서 모두 호출   

   App.js = Header.js + Main.js + Footer.js   

   App.js에서 name='홍길동' , color='blue' 값을 넘깁니다.   
   <br>
   App.js - 스프레드 연산자로 여러개의 값을 전달
   ```javascript
      function App() {

         const mainProps = {
            name : '홍',
            location : '서울시',
            color : 'blue',
            list : ['빵','치킨','돈까스']
         }

         return (
            <div>
               <Header></Header>
               <Main {...mainProps}></Main>  //스프레드 연산자
               <Footer></Footer>
            </div>
         );
      }

      export default App;
   ```   
   ...mainProps인 스프레드 연산자로 넘겼습니다.   
   <br>
   main.js
   ```javascript
      const Main = ({name, location, color, list}) => {
         return (
            <div style={{color}}>  //스타일 속성값으로 지정
               {name}은 {location}에 거주합니다. 
               좋아하는 음식 수는 {list.length}개 입니다.
            </div>
         );
      }

      export default Main;
   ```
   <br>
   Header.js
   ```javascript
      const Header = () => {
         return(
            <div>
               <h1>Header!!</h1>
               <hr/>
            </div>
         )
      }

      export default Header;
   ```   
   <br>
   Footer.js
   ```javascript
      const Footer = () => {
         return (
            <div>
               <h1>Footer!!</h1>
            </div>
         );
      }

      export default Footer;
   ```   