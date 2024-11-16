---
layout: single
title: parse와 stringify
categories: PROJECT
tag: []
---

1. # 각각의 형태

   parse한 형태
   ```javascript
      키 : "값"
   ```
   키는 하나의 객체로 작용하기 때문에 `" "`를 사용하지 않습니다. 그렇기 때문에 자바스크립트에서 키를 이용해서 값에 접근이 가능합니다.   

   stringify한 형태   
   ```javascript
      "키" : "값"
   ```
   키와 값에 전부 따옴표가 붙어 문자 형태가 됩니다.   

   <>

1. # Parsing (JSON.parse)
   parse는 JSON의 문자열 형태에서 자바스크립트 __객체나 배열로 변환__ 할 때 사용합니다.   

   1. 서버로부터 JSON 데이터를 받을 때   
   ```javascript
      fetch('https://api.example.com/data')
      .then(response => response.text()) // JSON 문자열로 응답을 받음
      .then(jsonString => {
         const data = JSON.parse(jsonString); // JSON 문자열을 JavaScript 객체로 변환
         console.log(data);
      });
   ```

   1. 파일에서 JSON 데이터를 읽어올 때   
   ```javascript
      const fs = require('fs');

      fs.readFile('data.json', 'utf-8', (err, jsonString) => {
         if (err) throw err;
         const data = JSON.parse(jsonString); // JSON 문자열을 객체로 변환
         console.log(data);
      });
   ```

   1. 로컬 스토리지에서 데이터를 읽을 때   
   ```javascript
      // 로컬 스토리지에서 데이터 가져오기
      const jsonString = localStorage.getItem('user');
      const user = JSON.parse(jsonString); // 문자열을 객체로 변환
      console.log(user.name); // 객체에서 데이터 접근
   ```

1. # Stringify (JSON.stringify)
   JavaScript 객체나 배열을 JSON __문자열로 변환__ 할 때 사용합니다.   

   1. 서버로 데이터를 보낼 때   
   ```javascript
      const user = { name: "Alice", age: 25 };

      // 객체를 JSON 문자열로 변환
      axios.post('https://api.example.com/users', JSON.stringify(user), {
         headers: {
            'Content-Type': 'application/json'
         }
      });
   ```

   1. 파일에 데이터를 저장할 때
   ```javascript
       const fs = require('fs');

      const data = { name: "Alice", age: 25 };

      // 객체를 JSON 문자열로 변환
      const jsonString = JSON.stringify(data);

      fs.writeFile('data.json', jsonString, (err) => {
         if (err) throw err;
         console.log('Data saved!');
      });
   ```

   1. 로컬 스토리지에 데이터를 저장할 때   
   ```javascript
      const user = { name: "Bob", age: 30 };

      // 객체를 JSON 문자열로 변환 후 저장
      localStorage.setItem('user', JSON.stringify(user));
   ```

1. # 결론
   받아서 사용할 때는 시스템이 인식을 해야하기 때문에 객체나 배열로 변환해야하고 이때 사용하는 것 : parse   
   보낼 때는 http 프로토콜로 데이터를 전송하기 때문에 문자열로 데이터를 전송 : stringify   

   사용할 땐 parse, 보낼 땐 stringify   