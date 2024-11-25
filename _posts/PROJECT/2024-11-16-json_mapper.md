---
layout: single
title: json으로 받은 파일을 mappper로 insert시키기
categories: PROJECT
tag: []
---

1. # react의 클라이언트 쪽

   객체 배열 형태로 주로 api로 데이터를 받으면 이런 형태입니다.   

   ```javascript
      let exam = [
            {name: 'aa', age: 23},
            {name: 'bb', age: 33},
            {name: 'cc', age: 18},
         ]

      await mapapi.savePharmDatas(exam); 
   ```
   전송할 때는 stringify로 JSON으로 문자열화 시킨다고 알고 있는데 그냥 자바스크립트의 객체 형태로 전송해야 서버쪽에서 데이터를 받았습니다.   

1. # 데이터를 받는 서버쪽
   ```javascript
      @PostMapping("/savePharmDatas")
      public  ResponseEntity<String> savePharmDatas(@RequestBody List<Map<String,Object>> pharmData) {

         int result = examService.saveData(pharmData);

         return new ResponseEntity<>("OK", HttpStatus.OK);
      }
   ```   
   자바스크립트 객체 배열을 받을 때는 List와 Map으로 받습니다.   
   객체의 값은 Map이 받게 배열의 값은 List가 받게 됩니다.

1. # Mapper에서 insert

   List 값을 넣기 위해서 foreac문을 사용합니다.   

   ```javascript
      <insert id="saveData" parameterType="List">
         insert into example (name, age) values 
         <foreach collection="list" item="item" separator=",">
            (#{item.name}, #{item.age})
         </foreach>
      </insert>
   ```   
   1)collection="list": 반복의 대상이 되는 데이터 집합을 나타냅니다. 여기서는 list라는 이름의 데이터 컬렉션을 순회합니다.   
   2)item="item": 반복에서 현재 처리 중인 요소를 나타냅니다. 각 반복에서 item이라는 변수에 컬렉션의 각 요소가 할당됩니다.   
   3)separator=",": 반복된 요소들을 나열할 때 구분자로 사용됩니다. 예를 들어, 출력이 item1, item2, item3 형태가 됩니다.   

   ex)   
   ```
      list = ["apple", "banana", "cherry"]

      <foreach collection="list" item="item" separator=",">
         {{item}}
      </foreach>
   ```
