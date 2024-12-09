---
layout: single
title: webrtc 이슈
categories: PROJECT
tag: []
---

1. # mentor

   <img src="../../imgs/project/webrtc_issu_captin.png" style="border:3px solid black;border-radius:9px;width:500px">   

   mentor 순서를 가장 앞에 오게 -> join으로 인식 나머지 event로 값을 받는다 어떻게 해결?

   mentor가 가장 먼저 join한 경우의 msg
   ```javascript   
      Object =>
         description : "test"
         id : 6019592257267288 //mentor 자신의 정보
         private_id : 2096999191
         publishers : Array(0) //기존 방에 있는 사람들의 정보
            length : 0
            [[Prototype]] : Array(0)
         room : 4545612
         videoroom : "joined"
            [[Prototype]] : Object

   ```
   publishers는 기존에 있는 사람들 정보고 여기 display에 username이 있다. join한 당사자는 그 페이지로 접속한 당사자이기 때문에 username이 초기 설정한 아이디

   subscriber가 join한 경우의 msg   
   ```javascript
      Object =>
         description : "test" 
         id : 1801972384065663  //subscriber의 정보
         private_id : 364008349  
         publishers : Array(1)  //기존 방에 있는 사람들의 정보
            0 : {id: 6019592257267288, display: 'mentor', audio_codec: 'opus', video_codec: 'vp8', streams: Array(2), …}   
            length : 1
            [[Prototype]] : Array(0)
         room : 4545612 
         videoroom : "joined"
         [[Prototype]] : Object
   ```

   publishers의 display가 아이디

   "mentor"인 경우만 publishOwnFeed()으로 화면을 켬



1. # 브라우저가 바뀌면 화면을 불러오지 못 한다
   세션 문제? 원격 스트림 문제, http요소 문제, 비디오 코덱 문제, 방화벽 문제, cors, 브라우저 호환성 다 아니다

   내 컴퓨터에서 최초 방을 만든 브라우저로 실행하면 다 된다. 그런데 브라우저를 옮기거나 다른 localhost로 접속한 컴퓨터에선 화면을 못 불러온다

   => 웹호스팅(github page)로 로딩해서 실행


1. # 변수 타입변환은 전역으로

   ```javascript
      var room = myroom

      function f1(){
          var data = {
            room : Number(room),
            //또는 
            room : ParseInt(room)
          }
      }
   ```   
   만약 room값이 해당 f1 함수 안에서만 사용하는 것이라면 함수 안에서 형변환 하여 사용해도 무방하지만,   
   만약 다른 곳에서도 room 변수를 사용한다면 전역으로 타입변환을 해야한다. room이 사용된 함수마다 다른게 인식할 수 있기 때문이다.   
   __눈에 보이는 결과가 같다고 컴퓨터가 모든 결과를 같다고 인식하지 않는다.__   

   ```javascript
      //전역으로 타입 변환
      var room = Number(myroom);  
      //또는 
      var room = parseInt(myroom);

      function f1(){
         var data = {
            room : room //여기 room 값과
         }
      }

      function f1(){
         var data2 = {
            room2 : room //여기 room 값이 일치
         } 
      }

   ```

1. # One To Many 구성

   join일 때와 event일 때 구독과 출판을 각각 조건에 맞게 입력