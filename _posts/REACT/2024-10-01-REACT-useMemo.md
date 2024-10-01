---
layout: single
title: useMemo
categories: REACT
tab: 
---

1. # useMemo
   useMemo는 React에서 제공하는 Hook 중 하나로, 값을 메모라이즈하여 불필요한 재계산을 방지하고 성능을 향상시키는 데 사용됩니다.

   **메모라이즈(Memoization)**란 이전에 계산된 값을 저장해 두었다가, 동일한 입력값으로 함수가 다시 호출될 때 저장된 값을 반환하는 기법입니다. 즉, 같은 계산을 반복하지 않고 이전에 계산한 결과를 재사용하여 성능을 향상시킵니다.

1. # 예시
   1)useMemo 사용 전
   ```javascript   
      import {useMemo, useState} from 'react'

      let UseMemoEx = () => {

         const [list, setList] = useState([1,2,3,4]);
         const [str, setStr] = useState('합계');
         
         let getAddResult = () => {
            let tot = 0;
            list.forEach((v,i,a) => tot += v)
            console.log("getAddResult안의 tot:",tot)
            return tot;
         }

         return (
            <div>
               <button onClick={()=>{setStr('안녕')}}>문자 변경</button>
               <button onClick={()=>{setList([...list,5])}}>리스트 값 추가</button>
               <br/>
               {list.map((v,i) => {
                  return <h3 key={i}>{v}</h3>
               })}
               <div>
                  {str} : {getAddResult()}
               </div>
            </div>
         )
      }

      export default UseMemoEx;
   ```
   문자 변경을 클릭하면 setStr 값이 변경되어 {str}이 속해있는 컴포넌트는 재렌더링이 되는데 이때, getAddResult()이 호출됩니다.   
   이런 경우, getAddResult() 함수 호출을 특정 경우에만 실행되게 할 수 있습니다.   

   ```javascript
      -선언-
      //useMemo('어떤 함수를 메모할 것인가','언제 실행되게 할 것인가')
      const addResult = useMemo(() => getAddResult(),[list]) //list가 변경되었을 때 getAddResult()를 실행

      //useMemo('어떤 함수를 메모할 것인가','언제 실행되게 할 것인가')
      const addResult = useMemo(() => {
         getAddResult()
      } ,[list]) //list가 변경되었을 때 getAddResult()를 실행

      -호출-
      변경 전 {str} : {getAddResult()} =>
      변경 후 {str} : {addResult}
   ```
   getAddResult함수를 list가 변경되었을 때만 실행되게 합니다.   

   <span style="color:red">*순서 중요</span>   
   useMemo에 들어가는 함수는 해당 함수 선언 이후에 와야 합니다.   

   2)useMemo 사용 후
   ```javascript   
      import {useMemo, useState} from 'react'

      let UseMemoEx = () => {

         const [list, setList] = useState([1,2,3,4]);
         const [str, setStr] = useState('합계');
         
         let getAddResult = () => {
            let tot = 0;
            list.forEach((v,i,a) => tot += v)
            console.log("getAddResult안의 tot:",tot)
            return tot;
         }
         
         //useMemo('어떤 함수를 메모할 것인가','언제 실행되게 할 것인가')
         const addResult = useMemo(() => getAddResult(),[list]) //list가 변경되었을 때 getAddResult()를 실행

         return (
            <div>
               <button onClick={()=>{setStr('안녕')}}>문자 변경</button>
               <button onClick={()=>{setList([...list,5])}}>리스트 값 추가</button>
               <br/>
               {list.map((v,i) => {
                  return <h3 key={i}>{v}</h3>
               })}
               <div>
                  {/* {str} : {getAddResult()} */}  
                  {str} : {addResult}
               </div>
            </div>
         )
      }

      export default UseMemoEx;

   ```

