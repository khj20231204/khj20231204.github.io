---
layout: single
title: 매개변수로 전달은 객체, 받을 땐 하나의 변수
categories: REACT
tab: 
---

1. # 매개변수의 전달 형태
   전달은 3개의 변수로 이루어진 객체를 전달하고 받을 땐, 하나의 변수로 받는 경우   

   리액트에서 updateUser 함수처럼 매개변수로 객체를 전달하고, 함수 내부에서 그 객체를 하나의 변수로 받아 사용하는 것은 완전히 가능하고 일반적인 방식입니다.   

   자바스크립트 객체의 특징: 자바스크립트 객체는 key-value 쌍으로 이루어진 데이터 집합입니다. 하나의 객체 안에 여러 개의 속성(key)과 값(value)을 담을 수 있기 때문에, 복잡한 데이터를 효율적으로 관리할 수 있습니다.   
   함수의 매개변수: 자바스크립트 함수는 매개변수로 다양한 타입의 값을 받을 수 있습니다. 그 중 하나가 객체입니다. 객체를 매개변수로 전달하면, 함수 내부에서 그 객체의 속성에 접근하여 값을 사용할 수 있습니다.   

   ```javascript

      export const update = (data) => api.put(`users/update`, data); //비동기로 form을 data로 전달

      const updateUser = async (form) => { //하나의 매개변수로 받음
         response = await auth.update(form);
      };

      updateUser({userId, userPw, email}); //객체를 전달
   ```