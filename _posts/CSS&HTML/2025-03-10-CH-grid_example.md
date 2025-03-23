---
layout: single
title: (CSS)grid 예시시
categories: CSS&HTML
tag: []
---

1. # Grid 속성 정리
   부모 요소(Grid Container) 속성   

   |  속성  |   설명   |
   |:------:|:--------:|
   |display: grid|그리드 컨테이너 생성|
   |grid-template-columns|열 크기 설정 (1fr, 100px, auto 등)|
   |grid-template-rows|행 크기 설정|
   |gap|행과 열 사이의 간격|
   |justify-content|전체 그리드 정렬 (가로 방향)|
   |align-content|전체 그리드 정렬 (세로 방향)|

   자식 요소(Grid Item) 속성   

   |  속성  |   설명   |
   |:------:|:--------:|
   |grid-column|아이템이 차지할 열 범위 지정 (grid-column: 1 / 3)|
   |grid-row|아이템이 차지할 행 범위 지정 (grid-row: 2 / 4)|
   |justify-self|개별 아이템 정렬 (가로)|
   |align-self|개별 아이템 정렬 (세로)|

1. # Grid 예시

   그리드 컨테이너 내부에 있는 자식 요소들이 기본적으로 1칸씩 차지합니다.   
   ```html
      <div class="grid-container">
         <div class="item">DIV 1</div>
         <span class="item">SPAN 2</span>
         <img class="item" src="image.jpg" alt="IMG 3">
      </div>
   ```   
   div, span, img, 등.. 1칸씩 차지   

   ```html
      <!DOCTYPE html>
      <html lang="ko">
      <head>
         <meta charset="UTF-8">
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
         <title>CSS Grid 예제</title>
         <style>
            .container {
                  display: grid; 
                  grid-template-columns: 1fr 2fr 1fr; /* 3개의 열: 첫 번째와 세 번째는 같고, 두 번째는 두 배 크기 */
                  grid-template-rows: 100px 150px 100px; /* 3개의 행: 높이 지정 */
                  gap: 10px; /* 각 셀 사이의 간격 */
                  background-color: lightgray;
                  padding: 10px;
            }

            .item {
                  background-color: steelblue;
                  color: white;
                  display: flex;
                  align-items: center;
                  justify-content: center;
                  font-size: 20px;
            }

            /* 특정 아이템 위치 지정 */
            .item1 {
                  grid-column: 1 / 3; /* 1번째 열부터 3번째 열까지 차지 */
                  grid-row: 1 / 2; /* 1번째 행에 위치 */
            }

            .item2 {
                  grid-column: 3 / 4; /* 3번째 열에 위치 */
                  grid-row: 1 / 3; /* 1~2번째 행을 차지 */
            }

            .item3 {
                  grid-column: 1 / 2; /* 1번째 열에 위치 */
                  grid-row: 2 / 4; /* 2~3번째 행을 차지 */
            }

            .item4 {
                  grid-column: 2 / 3; /* 2번째 열에 위치 */
                  grid-row: 2 / 3; /* 2번째 행에 위치 */
            }

            .item5 {
                  grid-column: 2 / 4; /* 2~3번째 열을 차지 */
                  grid-row: 3 / 4; /* 3번째 행에 위치 */
            }
         </style>
      </head>
      <body>
         <div class="container">
            <div class="item item1">1</div>
            <div class="item item2">2</div>
            <div class="item item3">3</div>
            <div class="item item4">4</div>
            <div class="item item5">5</div>
         </div>
      </body>
      </html>

   ```