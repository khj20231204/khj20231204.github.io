---
layout: single
title: find와 filter
categories: JS
tag: []
---
 
1. # find
   목적: 배열에서 주어진 __조건에 맞는 첫 번째 요소__ 를 찾아 반환합니다.   
   반환값: 조건에 맞는 요소를 찾으면 해당 요소를 반환하고, 없으면 undefined를 반환합니다.   

   조건을 만족하는 요소를 반환 하는 메소드   
   ```javascript
      const shoesData = [
         { id: 1, name: '운동화', price: 50000 },
         { id: 2, name: '구두', price: 80000 },
         { id: 3, name: '샌들', price: 30000 }
      ];

      // 찾고 싶은 id 값
      const idCheck = 2;

      // find 메서드를 사용하여 id가 2인 객체 찾기
      const shoes = shoesData.find((x) => x.id === idCheck);

      console.log(shoes); // { id: 2, name: '구두', price: 80000 }
   ```   
   x.id === id의 결과는 true나 false로 boolean을 반환할 것 같은데 조건을 만족하는 shoesData의 객체를 리턴합니다. 이것은 find메소드의 반환타입이 조건을 만족하는 해당 요소이기 때문입니다.   

1. # filter
   목적: 배열에서 주어진 __조건에 맞는 모든 요소를 추출__ 하여 새로운 배열을 생성합니다.   
   반환값: 조건에 맞는 요소들로 구성된 새로운 배열을 반환합니다. 조건에 맞는 요소가 없으면 빈 배열을 반환합니다.   

   조건에 맞는 요소를 반환하는 메소드   
   ```javascript
      const shoesData = [
         { id: 1, name: '운동화', price: 50000 },
         { id: 2, name: '구두', price: 80000 },
         { id: 3, name: '샌들', price: 30000 }
      ];

      // 찾고 싶은 id 값
      const idCheck = 2;

      // find 메서드를 사용하여 id가 2인 객체 찾기
      const shoes = shoesData.filter((x) => {
         return (
         x.id >= idCheck
         );
      });

      console.log(shoes);

      결과값:
      0 : {id: 2, name: '구두', price: 80000}
      1 : {id: 3, name: '샌들', price: 30000}
   ```   
   id가 2보다 큰 객체 '구두'와 '샌들'을 리턴합니다.   