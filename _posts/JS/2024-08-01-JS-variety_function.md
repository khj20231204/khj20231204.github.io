---
layout: single
title: 다양한 함수들
categories: JS
tag: []
---
 
1. # Map
   key와 value의 형태로 데이터를 저장하고 가져옵니다.   
   key는 유일한 값이며, value는 중복을 허용합니다.   

   new Map() – 맵 생성   
   map.set(key, value) – key와 value를 저장
   map.get(key) – key에 해당하는 value을 반환. key가 존재하지 않으면 undefined를 반환
   map.has(key) – key의 존재 유무확인, 존재하면 true, 존재하지 않으면 false
   map.delete(key) – key에 해당하는 value를 삭제
   map.clear() – 맵 안의 모든 요소를 제거
   map.size – 요소의 개수를 반환

1. # Set
   Set = '집합' 이라고 생각할 수 있습니다. 순서 없이 중복된 값을 허용하지 않습니다.   

   new Set([iterable]) – 셋 생성.
   set.add(value) – 값을 추가하고 셋 자신을 반환
   set.delete(value) – 값을 제거
   set.has(value) – 셋 내에 값이 존재하면 true, 아니면 false를 반환
   set.clear() – 셋을 비움
   set.size – 셋의 크기 반환.

1. # foreach
   ```
      arr.forEach(function(v,i,a){
         ...
      })

      v:배열 값
      i:인덱스
      a:배열 
   ```
   function의 인자로 v,i,a개의 값을 받아옵니다. v는 배열 값, i는 인덱스, a는 배열입니다. v는 필수 인자로 작용하고 i와 a는 필요에 따른 선택 항목입니다.

   __배열__ 에 forEach사용
   ```js
      let arr2 = [1,2,3,4]
      arr2.forEach((v,i,a) => {
         console.log(`array v:${v} ,i:${i} ,a:${a}`)
      })
      /*
      array v:1 ,i:0 ,a:1,2,3,4
      array v:2 ,i:1 ,a:1,2,3,4
      array v:3 ,i:2 ,a:1,2,3,4
      array v:4 ,i:3 ,a:1,2,3,4
      */
   ```   

   __Set__ 에 forEach사용   
   ```javascript
      let map2 = new Map([
         [11,'홍길동'],[12,'임꺽정'],[13,'이순신']
      ])

      map2.set(14,'장보고') //set으로 키와 value 추가

      map2.forEach((v,i,a) => {
         console.log(`map v:${v} ,i:${i} ,a:${a}`)
      })
      /*
      map v:홍길동 ,i:11 ,a:[object Map]
      map v:임꺽정 ,i:12 ,a:[object Map]
      map v:이순신 ,i:13 ,a:[object Map]
      map v:장보고 ,i:14 ,a:[object Map]
      */
   ```

   __Map__ 에 forEach사용
   ```javascript
      let set2 = new Set([1,2,3,4])
      set2.forEach((v,i,a) => {
         console.log(`set v:${v} ,i:${i} ,a:${a}`)
      })
      /*
      set v:1 ,i:1 ,a:[object Set]
      set v:2 ,i:2 ,a:[object Set]
      set v:3 ,i:3 ,a:[object Set]
      set v:4 ,i:4 ,a:[object Set]
      */
   ```