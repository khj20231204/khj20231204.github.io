---
layout: single
title: metacoding 요약
categories: REACT
tab: [react]
---

1. # 실행 순서
   npm start →   
   index.js : index.html파일의 root를 찾는다   
   ```javascript
      const root = ReactDOM.createRoot(document.getElementById('root')); //index.html파일에서 id = root를 찾는다
      root.render(  //index.html의 root에 밑에 부분을 랜더링
         <React.StrictMode>
            <App />
         </React.StrictMode>
      );
   ```
   → App.js   

   __index.js에서 index.html에 App.js를 랜더링__   

   *React : 엔진이다. 데이터변경을 감지해서 UI를 그려주는   

   __조건부__   
   ```javascript
      <h2> {a === 10 ? 10입니다} </h2>
   ```

1. # 함수 실행
   이벤트에 함수를 연결하는 건 주소를 바인딩하는 것
   ```javascript
      let [list, setList] = useState([1,2,3,4]);

      let addList = () => {
         let sum = 0 ;
         list.forEach(i => sum = sum+1)

         console.log("sum:"+sum);

         return sum;
      }

      return (
         <div>
            합계 : {addList()} //결과를 바로 돌려줄 때는 함수 실행
            <div onClick={addList}>클릭</div> //이벤트에 연결할 땐 바인딩
         </div>
      );
   ```   
   합계 : {addList()}   
   addList()는 addList의 함수 실행 하는 것으로 return값을 받아 옵니다.   

   `<div onClick={addList}>클릭</div>`
   이벤트에 함수를 연결할 때는 주소로 바인딩을 해줍니다.   

1. # export
   ```javascript
      import Sub from './Sub'; //같은 폴더 위치의 default export
      import Top from './page/Top';  //page폴더의 위치의 default export
      import { num } from './Sub';  //named export
   ```

   default export는 컴포넌트당 1개만 가능합니다. 변수나 함수의 named export를 사용하는 경우 { }를 붙입니다.
   ```javascript
      let num = 1;

      const Test = () => {
         
         let num3 = 10;

         return (
            <div>
               
            </div>
         );
      };

      const Test2 = () => {

         let num2 = 5;

         return (
            <></>
         )
      }

      export { num , Test};  //추가적인 export 방법
      export default Test2; //default의 export는 1개밖에 못 함 
   ```
   num을 export할 때 { }를 사용하고 import 할 때도 { }를 사용합니다.   

1. # 빈 배열 만들기
   ```javascript
      let array = Array.from({length:5}).fill(''); //빈 배열 생성

      let array = Array.from({length:5}).fill(5);  //5로 초기화
   ```