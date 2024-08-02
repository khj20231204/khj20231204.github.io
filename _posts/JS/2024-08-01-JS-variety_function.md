---
layout: single
title: 다양한 함수들
categories: JS
tag: []
---
 
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

   ```js
      var arr = [13,34,54,5];

      arr.forEach(function(v,i,a){
         console.log("v:"+v);
      });

      arr.forEach(function(v,i,a){
         console.log("i:"+i);
      })

      arr.forEach(function(v,i,a){
         console.log("a:"+a);
      })
   ```