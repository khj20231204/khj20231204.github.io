---
layout: single
title: Context API
categories: REACT
tab: 
---

1. # Context API
   부모 state를 저장해서 자식에게 전달하는 기능을 합니다. React는 기본적으로 부모에서 자식으로 데이터가 흐르는 단방향 데이터 흐름을 따릅니다. 즉, 부모 컴포넌트에서 자식 컴포넌트로 props를 통해 데이터를 전달하고, 자식 컴포넌트는 props를 통해 받은 데이터를 기반으로 자신의 상태를 변경할 수 있지만, 그 반대는 되지 않습니다. useContext는 부모 컴포넌트에서 제공한 값을 자식 컴포넌트에서 사용할 수 있도록 해주는 역할을 합니다. 즉, 부모에서 자식으로 데이터를 전달하는 통로 역할을 할 뿐, 자식에서 부모로 데이터를 역전파하는 기능은 제공하지 않습니다.   

1. # 부모 컴포넌트

   1)createContext를 선언. export해주기!!🪓   
   2)Provider를 붙이고 value에 state를 입력한다.🧹
   3)state를 넘기 컴포넌트를 둘러싼다.💉   
   

   -App.js-   
   ```java
      {/*
      1)App에 있는 state를 공유하겠다
      2)context선언
      3)선언한 context로 감싸기
      */}

      export let Context1 = createContext() //1)🪓context 객체 생성

      function App() {

      let [stock] = useState([10,11,12]);
      let [shoes] = useState('shoes');

      let {childValue} = useContext(ChildContext)

      return (
         <div className="App">
            <h1>App.js home</h1>

            <h2>{childValue}</h2>

            <Routes>
               <Route path="/detail" element={
                  <Context1.Provider value={{ stock,shoes }}> {/* 
                  2)🧹Provider를 붙이고 value에 state를 저장한다
                  3)💉context로 둘러싼다 */}
                  <Details/> {/* 여기 안의 모든 컴포넌트는 재고, shoes 사용가능 */}
                  </Context1.Provider>
               }></Route>
            </Routes>
         </div>
      );
      }
      export default App;
   ```

1. # 자식 컴포넌트
   자식 컴포넌트에서 부모 컴포넌트에서 보낸 state를 사용합니다.   

   1)부모에서 선언한 context import하기🔺
   2)부모에서 선언한 useContext 변수 가져오기🔸   

   -Details.js-   
   ```java
      import { Context1 } from './App'; //1)🔺Context1 임포트

      const Details = () => {

         /* 2)🔸Context1을 넣어서 useContext:Context를 사용하겠다는 뜻
         /* 변수 또는 구조분해 할당으로 useContext 값을 가져온다 */
         let v = useContext(Context1) 
         let {stock, shoes} = useContext(Context1)

         return (
            <div>
               <h1>Details home</h1>
               {stock.map((v,i)=> <h2>{v}</h2> )}
               {shoes}
            </div>
         );
      };

      export default Details;
   ```
