---
layout: single
title: 제어된 컴포넌트
categories: REACT(Lesson)
tag: []
author_profile: false
---

1. # 제어된 컴포넌트
   리액트에서 input 요소의 value를 관리할 때 onChange 이벤트 핸들러를 사용하는 이유는 주로 "제어된 컴포넌트"(Controlled Component) 개념과 관련이 있습니다.  
   제어된 컴포넌트 (Controlled Component)   
   리액트에서는 폼 요소의 값을 상태(state)로 관리하는 것이 일반적입니다. 이 방법을 통해 입력 값이 컴포넌트의 상태와 일치하도록 유지할 수 있습니다. 제어된 컴포넌트에서는 입력값을 상태로 관리하고, 사용자가 입력할 때마다 onChange 이벤트 핸들러를 통해 상태를 업데이트합니다.   
   
   이렇게 하면 다음과 같은 이점이 있습니다   
   1)값의 일관성 유지: 입력 필드의 값이 상태와 항상 일치하므로, 입력 필드의 값이 프로그램matically 변경되더라도 상태와 일관성을 유지할 수 있습니다.   
   2)입력 검증 및 변형: 사용자가 입력하는 값에 대해 실시간으로 검증하거나 변형할 수 있습니다. 예를 들어, 입력이 특정 형식이어야 하는 경우 유효성을 검사하고 오류 메시지를 표시할 수 있습니다.   
   3)상태 관리의 일관성: 폼 상태를 한 곳에서 일관되게 관리할 수 있습니다. 상태 변화에 따라 UI가 자동으로 업데이트되며, 이는 복잡한 폼을 관리하는 데 유리합니다.   

1. # 기본 HTML vs 리액트
   HTML의 기본 `<input type="text">`는 사용자가 입력할 때마다 value가 자동으로 업데이트됩니다. 이 경우 value 속성은 입력 필드의 현재 값을 나타내며, 입력 필드의 값을 직접 조작할 수 있습니다. 반면, 리액트에서는 상태를 통해 값을 제어하므로, 입력 필드의 값을 상태와 연결하여 제어합니다. 이 과정에서 onChange 이벤트 핸들러가 중요한 역할을 하게 됩니다.   

   ```cs
      import React, { useState } from 'react';

      function MyForm() {
         const [value, setValue] = useState('');

         const handleChange = (event) => {
            setValue(event.target.value);
         };

         return (
            <div>
               <input type="text" value={value} onChange={handleChange} />
               <p>입력한 값: {value}</p>
            </div>
         );
      }
      export default MyForm;
   ```   
   value는 컴포넌트의 상태로 관리되며, onChange 이벤트 핸들러가 사용자의 입력을 처리하고 상태를 업데이트합니다. 이로 인해 입력 필드의 값이 상태와 동기화되며, 화면에 입력한 값이 즉시 반영됩니다.   

   결론적으로, 리액트에서는 상태를 통해 입력 값을 제어하기 위해 onChange 이벤트 핸들러를 사용하며, 이는 제어된 컴포넌트를 구현하는 데 필수적입니다.   