---
layout: single
title: submit버튼과 target
categories: REACT
tab: 
---

1. # submit과 target
   `<form>` 태그 안에서 action을 통해 서버쪽으로 데이터를 넘기고 싶을 때 2가지 버튼 형식이 존재합니다.   

   ```javascript
      const onLogin = (e) => {
         e.preventDefault(); //submit이라서 막는다

         const form = e.target; 

         console.log(e);
      }

      //방식 - 1
      <form>
         <button onClick={(e) => onLogin(e)}>로그인</button>
      </from>

      //방식 - 2
      <form onSubmit={(e) => onLogin(e)}>
         <button type="submit">로그인</button>
      </form>
   ```

   버튼으로 넘기는 경우 => target : button.form_btn   
   form에서 onSubmit으로 넘기는 경우 => target : form   

   form의 action을 통해 데이터를 서버로 넘기는 것이 목적이라면 button의 기본값이 submit이기 때문에 방식1, 2 모두 action의 값으로 데이터가 넘어가게 됩니다.   
   
   하지만 만약, 이벤트 객체 e를 가지고 target속성을 통해 form의 값을 가져와서 name와 password등의 값들을 가져오기 위해서는 form의 submit 이벤트로 넘겨야 합니다.   