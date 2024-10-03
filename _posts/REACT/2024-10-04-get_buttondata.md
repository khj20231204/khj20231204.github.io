---
layout: single
title: 버튼으로 값 가져오는 방법
categories: REACT
tab: [react]
---

1. 버튼 클리시
```
   import React, { useState } from 'react';

      function MyComponent() {
      const [inputValue, setInputValue] = useState('');

      const handleChange = (event) => {
         setInputValue(event.target.value);
      };

      const hand   
      leClick = () => {
         alert(`입력한 값: ${inputValue}`);
      };

      return (
         <div>
            <input type="text" value={inputValue} onChange={handleChange} />
            <button onClick={handleClick}>값 출력</button>
         </div>
      );
      }
```

1. #  useState 훅으로 상태 관리하기
JavaScript
import React, { useState } from 'react';

function MyComponent() {
  const [inputValue, setInputValue] = useState('');

  const handleChange = (event) => {
    setInputValue(event.target.value);
  };

  return (
    <div>
      <input type="text" value={inputValue} onChange={   
handleChange} />
      <p>입력한 값: {inputValue}</p>
    </div>
  );
}