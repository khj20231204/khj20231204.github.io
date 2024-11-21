---
layout: single
title: useNaviate사용
categories: REACT
tab: 
---

1. # useNavigate
   useNavaigate는 훅으로 다른 페이지로 이동을 하게 됩니다. 리액트에서 페이지 이동의 명령어로 Link to가 있습니다.   

   __useNaviagate__   
   프로그램적으로 페이지를 이동할 때 사용됩니다. 함수 호출로 페이지를 이동하거나 state의 상태값을 전달하거나 if, switch, 비동기 작업과 같은 동적 페이지 이동에 사용됩니다.   

   __Link to__   
   정적인 페이지 이동에 주로 사용됩니다. html의 `<a>` 태그와 유사한 역할을 합니다. 네비게이션바, 사이드바 등 단순 페이지를 링크하여 이동할 때 사용됩니다.   


1. # useNavigate 예제

   naviaget를 사용하여 state를 보내는 쪽   
   ```javascript
      //import
      import {useNavigate} from 'react-router-dom';
    
      //변수 선언
      const navigate = useNaviage();

      //사용, state전달
      const funct = () => {
         ...
         navigate('/mysite',{state:{key:value, key2:value2}})
         ...
      }
   ```

   mysite.jsx 페이지 - naviage를 받는 쪽   
   ```javascript
      //받을 땐 useLocation사용
      import {useLocation} from 'react-router-dom';

      //변수 선언
      const location = useLocation();

      //값을 받음
      const {key, key2} = location.state;
   ```

   값을 전달할 때는 useNaviate, 받을 땐  useLocation을 이용합니다.   

1. # Link to 예제

   html의 a태그와 같이 단순한 페이지 이동에 사용됩니다.   
   ```javascript
      import { Link } from 'react-router-dom';

      function Navbar() {
         return (
            <nav>
               <ul>
               <li><Link to="/home">홈</Link></li>
               <li><Link to="/about">소개</Link></li>
               <li><Link to="/contact">문의</Link></li>
               </ul>
            </nav>
         );
      }

   ```