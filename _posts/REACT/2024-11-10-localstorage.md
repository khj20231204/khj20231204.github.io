---
layout: single
title: localstorage 사용
categories: REACT
tab: 
---

1. # 사용법 🔊
   1. localStorage.setItem(key, value)로 저장하고, localStorage.getItem(key)로 불러온다.   
   1. 객체는 JSON.stringfy(value)로 JSON 형태의 문자열로 변환하여 저장하고, 불러온 후에는 JSON.parse(value)를 통해 다시 객체로 변환한다.   
   1. useEffect()를 사용하여 마운트되었을 때 불러오고, todoList나 id가 업데이트 되었을 때 저장한다.   
   1. localStorage의 값들은 문자열로 저장이 되기 때문에 숫자인 id 값을 불러올 때 parseInt()로 변환해서 사용한다.   

   => 객체는 파싱, 숫자는 parseInt👍   

localStorage에 데이터 저장하기   
```javascript
   
   useEffect(() => {
      localStorage.setItem('todoList', JSON.stringify(todoList));
      localStorage.setItem('id', id);
   }, [todoList, id]);
```

localStorage에서 데이터 불러오기   
```javascript

   let [todoList, setTodoList] = useState();
   let [id, setId] = useState();

   useEffect(() => {
      const localTodoList = localStorage.getItem('todoList');
      if (localTodoList) {
         setTodoList(JSON.parse(localTodoList));
      }
      
      const localId = localStorage.getItem('id');
      if (localId) {
         setId(parseInt(localId));
      }
   }, []);

```