---
layout: single
title: (CSS)배치(flex_items)
categories: CSS&HTML
tag: []
---

1. # flex-basis
   flex-basis는 __Flex아이템의 기본 크기__ 를 설정합니다.(flex-direction이 row일 때는 너비, column일 때는 높이).   
   
   ```cs
      .item {
         flex-basis: auto; /* 기본값 */
         /* flex-basis: 0; */
         /* flex-basis: 50%; */
         /* flex-basis: 300px; */
         /* flex-basis: 10rem; */
         /* flex-basis: content; */
      }
   ```   
   flex-basis값으로 width, height에 들어가는 각종 단위의 수가 들어갈 수 있고, 기본값은 auto입니다. auto를 설정한 경우 해당 아이템의 width값이 사용됩니다. content는 width를 따로 설정하지 않은 값과 같습니다.   

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="wvbmMmR" data-pen-title="flex_item_basis" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/wvbmMmR">
   flex_item_basis</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
      
   BBBBBBBBBB를 보면 flex-basis를 100px를 둔 경우 넓이가 BBBBBBBBBB 보다 작아도 크기가 BBBBBBBBBB의 크기에 맞춰집니다.   
   하지만 width를 100px를 둔 경우 넓이가 BBBBBBBBBB 보다 작기 때문에 작은 그 상태로 그대로 출력됩니다.   

1. # flex-Item속성 : flex-grow   
      "유연하게 늘리기" 기능이 가능합니다. flex-grow는 아이템이 flex-basis의 값보다 커질 수 있는지를 결정하는 속성입니다. flex-grow에는 숫자값이 들어가는데, 몇이든 일단 0보다 큰 값이 세팅이 되면 해당 아이템이 유연한(flexible) 박스로 변하고 원래의 크기보다 커지면 빈 공간을 메우게 됩니다. 기본값이 0이기 때문에, 따로 적용하기 전까지는 아이템이 늘어나지 않았습니다.   

      ```cs
         .item {
            flex-grow: 1;
            /* flex-grow: 0;  기본값 */
         }
      ```

1. # flex-Item속성 : order
   flex item의 순서를 설정합니다. 기본값은 0이고, 숫자가 작을수록 먼저 왼쪽에 위치하게 됩니다.   

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="bGJQyBP" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/bGJQyBP">
   ch05.item_order</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

