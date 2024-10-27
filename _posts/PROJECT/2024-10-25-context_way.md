---
layout: single
title: Context 사용
categories: PROJECT
tag: []
author_profile: false
---   

1. # 전체 폴더 구조와 설명

   <img src="../../imgs/project/context_use.png" style="border:3px solid black;border-radius:9px;width:700px">   

   ```javascript
      -App.js-

      import PharmacyPage from './pages/PharmacyPage';
      import { BrowserRouter, Routes, Route } from 'react-router-dom';
      import Login from './pages/Login';
      import About from './pages/About';
      import Join from './pages/Join';
      import User from './pages/User';
      import LoginContextProvider from './contexts/LoginContextProvider';

      function App() {
      return (
         <BrowserRouter>
            <LoginContextProvider>
            <Routes>
               <Route path="/" element={<PharmacyPage></PharmacyPage>}></Route>
               {/* PharmacyPage안에 Header와 PharMain에서도 context적용 */}
               <Route path="/about" element={<About></About>}></Route>
               <Route path="/join" element={<Join></Join>}></Route>
               <Route path="/login" element={<Login></Login>}></Route>
               <Route path="/user" element={<User></User>}></Route>
            </Routes>
            </LoginContextProvider>
         </BrowserRouter>
      );
      }

      export default App;
   ```
   Routes를 LoginContextProvider로 감싸면 Routes의 하위 컴포넌트들은 전부 LoginContextProvider에서 제공하는 state를 사용할 수 있다   
   

    ```javascript
      -PharmacyPage-

      import React from 'react';
      import PharMain from '../components/pharmacy/PharMain';
      import Header from '../components/Header/Header';
      import LoginContextConsumer from '../contexts/LoginContextConsumer';

      const PharmacyPage = () => {
         return (
            <div>
               <Header/>
               <PharMain></PharMain>
               <LoginContextConsumer /> //LoginContextConsumer 사용
            </div>
         );
      };

      export default PharmacyPage;
   ```
   LoginContextConsumer가 LoginContextProvider에서 제공하는 state를 사용한다