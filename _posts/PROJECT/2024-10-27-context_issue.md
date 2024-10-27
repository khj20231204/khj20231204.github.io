---
layout: single
title: React - Context 이슈
categories: PROJECT
tag: []
author_profile: false
---   

1. # 문제 발생 배경👨‍💻
   Home, Join, About, User등 프론트페이지에서 로그인 상태값을 가져오기 위해서 자식 컴포넌트들에게 직접 porps로 전달하기 보다는 Context를 생성하고 state를 전달하는 것이 효율적입니다. 때문에 Context를 사용하게 되었습니다.   
   물론 Context도 state값이 변하면 이를 사용하는 모든 자식 컴포넌트들도 재랜더링이 된다는 성능 이슈와 Context를 사용하고 있는 컴포넌트의 경우 재사용성이 어렵다는 문제점이 있지만 작은 프로젝트에서는 Redux까지 사용할 필요는 없기 때문에 Context를 사용했습니다.   

   ```javascript
      -LoginContextProvider.jsx-

      import React, { createContext, useState } from 'react';

      export const LoginContext = createContext();
      LoginContext.displayName = 'LoginContextName'

      const LoginContextProvider = ({ Children }) => {
         //context value : 로그인 여부, 로그아웃 함수
         const[isLogin, setLogin] = useState(false);

         const logout = () => {
            setLogin(false);
         }

         return (
            <div>
               <LoginContext.Provider value={{isLogin, logout}}>
                  {Children}
               </LoginContext.Provider>
            </div>
         );
      };

      export default LoginContextProvider;
   ```
   LoginContextProvider에서 Context를 생성 후 Provider를 해줌

   ```javascript
      -LoginContextConsumer.jsx-

      import React, { useContext } from 'react';
      import { LoginContext } from './LoginContextProvider';

      const LoginContextConsumer = () => {

         const { isLogin } = useContext(LoginContext);

         return (
            <div>
               <h2>LoginContextConsumer</h2>
         {/*     로그인 여부 : {isLogin ? '로그인' : '로그아웃'} */}

            </div>
         );
      };

      export default LoginContextConsumer;
   ```
   Context를 생성하고 state를 제공한 컴포넌트 LoginContextProvider를 import 후 사용 시 값을 불러오지 못 함   

   해당 코드가 문제가 발생한 코드입니다.   

1. # 문제 발생⛈️
   ContextProvider가 있는 부모 컴포넌트로 consumer가 존재하는 자식 컴포넌트를 둘러쌌는데 값을 제대로 전달받지 못 했습니다.

1. # 해결🌤️
   저 같은 경우 어떠한 기능에 대해 잘 모르는 상태에서 문제가 발생하면 먼저 문법적인 오류를 찾아봅니다. 그리고 값을 전달하는 과정에서 값을 제공하는 쪽과 받는 쪽의 커넥션 상태를 확인합니다. 일단 프로그램이 실행되고 JSX컴파일 과정에서 에러가 발생하지 않으면 오타를 찾는 것은 쉽지 않습니다. 

   지금의 에러와 같이 성공적으로 랜더링도 되고 콘솔에 아무런 에러 원인도 출력되지 않는데 값만 불러오지 못 하는 경우, 어느 부분에서 문제가 발생했는지 이슈 지점을 가장 먼저 찾아야 했습니다. Context의 경우는   
   1)Context를 생성하는 부분   
   2)Provider로 state값을 넘겨주는 부분   
   3)Context를 import해서 state값을 전달받아 사용하는 Consumer   
   4)App.js에서 Provider와 Consumer를 바인딩하는 부분   
   크게 4부분으로 분류가 가능합니다.   

   먼저 잘 동작하는 Context와 Provider, Consumer를 생성 후 해당 컴포넌트에 먼저 작성한 값들을 대입해서 에러 지점을 찾기위해 좁혀들어 갔습니다.   

   에러가 발생하는 Context와 잘 동작하는 Provider   
   에러가 발생하는 Provider와 잘 동작하는 Consumer  
   에러가 발생하는 Consumer와 잘 동작하는 Context   
   ...

   App에서의 컴포넌트 구성 등을 변화 시키며 정상적으로 동작할 때와 에러가 발생할 때를 구분 지으면 문제점을 찾아 갔습니다.   

   Context를 생성한 Provider에서 Consumer쪽으로 값을 제대로 전달하지 못 한다는 문제점을 발견 후, 정상코드와 에러코드를 동시에 비교를 했는데   

   똑같았습니다...✈️   

   이 부분에서 Render Props 개념이 무엇인지 알게 되었습니다.   

   Render Props란1️⃣   
   부모 컴포넌트에서 자식 컴포넌트로 단순히 state값만 넘기는 것이 아니라 Props로 JSX나 함수를 전달하여 코드의 재사용성과 유연성을 높이는 Reac의 문법 패턴입니다. 부모 컴포넌트의 코드를 자식이 받아서 필요한 부분만 변경 후 사용하는 커스터마이징이 된다는 점에서 복잡한 UI를 작은 컴포넌트 별로 독립화하여 재사용성과 유연성을 높이는 React의 성격과 잘 맞아 떨어지는 강력한 기능이라고 생각합니다.   

   그렇다면.. Render Props는 기능일 뿐 넘기는 변수를 작명하는 부분은 개발자들의 성격, 가독성, 회사별 변수 작명법 등을 고려하여 사용자에게 변수명을 만드는 것을 전적으로 위임해야 되지 않을까 생각합니다.   

   하지만, React는 Context를 사용할 때만큼은 children이란 프롭스의 변수명을 정해 놓았습니다. 'Children'이 아니라 'children' 입니다.   

   여기서 children이란2️⃣   
   컴포넌트의 태그 안에 들어있는 모든 자식 요소를 가리키게 됩니다. Reac.Children의 API로써 특별한 props입니다. children을 통해서 컴포넌트들을 유연하게 전달하고 관리할 수가 있습니다.   

   Context로 JSX나 함수를 넘기고 받을 때 Props로 children이 사용됩니다. children이 props에 속하긴 하지만 단순한 변수가 아니라 다양한 기능을 제공하는 API의 개념에 가깝습니다. 그렇기 때문에 '변수의 작명법'으로 간단히 생각하면 안되는 부분이였습니다. 자바에서는 함수의 매개변수로 값을 넘길 때 변수의 이름이 고정되는 경우는 경험해보지 못했지 때문에, 역시 react는 색다른 재미가 있습니다. 에러를 찾아가는 과정도 하나의 즐거움이므로👍

   결국, 6시간을 소비하게 만든 에러의 원인은 children을 Children으로 잘못 작성한데 있었습니다.   



   
