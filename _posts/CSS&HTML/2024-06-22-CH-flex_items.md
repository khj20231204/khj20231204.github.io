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

1. # flex-basis의 content/auto/숫자/0

   2. content   
   ```cs
      flex-basis: content;
   ```   
   아이템 안의 공간(여백)이 없어지고 글자(content)의 크기에 맞춰집니다.   

   2. AUTO   
   ```cs
      flex-basis: auto;
   ```   
   기존에 부모 컨테이너에 의한 크기든 브라우저에 제공되는 크기든 기존의 크기에 따릅니다.   
      
   2. 숫자   
   ```cs
      flex-basis: 100px;
   ```   
   width가 100px가 되는데, 글자(content)의 길이가 100px 보다 긴 경우 content에 맞춰집니다.   

   2. 0   
   ```cs
      flex-basis: 0;
   ```   
   아이템 안의 공간(여백)이 없어지는데 기존 auto 값에서 여백이 없었던 경우 기존 그 값이 그대로 유지됩니다.   
      
   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="wvbjzgm" data-pen-title="flex_basis_auto_zero" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/wvbjzgm">
   flex_basis_auto_zero</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

1. # flex-Item속성 : flex-grow   
   __container와 item 사이에 공간(여백)이 있는 경우 item 내부의 content(글자)를 제외한 공간을 늘려 container와 item들 사이의 공간을 없애는 기능__   
   item들을 container에 가득 채우기 위해 item 내부의 글자를 제외한 여백의 공간을 "유연하게 늘리기" 위한 기능입니다. flex-grow는 아이템이 flex-basis의 값보다 커질 수 있는지를 결정하는 속성입니다. flex-grow에는 숫자값이 들어가는데, 몇이든 일단 0보다 큰 값이 세팅이 되면 해당 아이템이 유연한(flexible) 박스로 변하고 원래의 크기보다 커지면 빈 공간을 메우게 됩니다. 기본값이 0이기 때문에, 따로 적용하기 전까지는 아이템이 늘어나지 않았습니다.   
   
   ```cs
      .item1{
         flex-grow: 1;
         /* flex-grow: 0; 기본값 */
      }
   ```   
   flex-grow에 들어가는 숫자의 의미는 flex-basis를 제외한 여백 부분을 flex-grow에 지정된 숫자의 비율로 나누어지게됩니다.   

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="bGyvJjQ" data-pen-title="flex_item_grow" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/bGyvJjQ">
   flex_item_grow</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>    
      
   flex-grow 값은 아이템의 __글자를 제외한__ 공백부분의 비율이 됩니다.   
   .item1의 첫번째, 두번째, 세번째 각각의 아이템의 flex-grow 값이 0.5, 0.5, 1 인데 이것은 1:1:2로 0.1,0.1,0.2 든 0.3,0.3,0.6 이든 10,10,20이든 숫자 값은 상관없이 각각의 비율에 따라 공백이 결정됩니다.   

   가장 상단은 item들이 container에 가득 차지 않아서 container 여백인 skyblue 색상이 보입니다. 이를 flex-grow 속성으로 각각 item들의 contetnt를 제외한 공간부분을 늘여 item들이 container에 가득차게 할 수 있습니다.   
   item2에서 첫번째와 세번째 item의 content를 길게 했을 경우 content를 제외한 여백의 비율을 전부 1:1:1:1로 맞추기 위해서 item의 길이는 전부 상이하게 됩니다.   
   item3에서도 item2와 마찬가지로 flex-gorw:1;로 설정했습니다. item2와 비교했을 때 content 글자의 길이가 비슷하기 때문에 item의 길이도 비슷하게 설정되었습니다.   

1. # flex-shrink   
   __container의 레이아웃을 아이템이 너무 커서 넘친 경우 이를 적절히 나눠서 줄이는 기능__   
   __flex-wrap:nowrap;으로 설정해야 적용!__   
   flex-grow와 쌍을 이루는 속성으로, 아이템이 flex-basis의 값보다 작아질 수 있는지를 결정합니다. flex-shrink는 숫자값이 들어가는데, 몇이든 일단 0보다 큰 값이 셋팅이 되면 해당 아이템이 유연한(flexible) 박스로 변하고 flex-basis보다 작아집니다. 기본값이 1이기 때문에 따로 셋팅하지 않아도 아이템이 flex-basis 보다 작아질 수 있습니다.   

   ```cs
      .item{
         flex-shink: 1; /* 기본값 */
      }
   ```    

   <p class="codepen" data-height="500" data-default-tab="html,result" data-slug-hash="BaererB" data-pen-title="flex_item_shrink" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/BaererB">
   flex_item_shrink</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>   
      
   container의 width: 600px;   
   item1의 flex-basis: 300px;로 아이템 1개당 300px로 총 300*3 = 900px이기 때문에 -300px를 해줘야 600px로 container안에 들어갈 수 있습니다.   
   item2의 flex-shrink비율은   
   
   ```cs      
      .item2:nth-child(1){
      flex-shrink:1;
      }

      .item2:nth-child(2){
      flex-shrink:3;
      }

      .item2:nth-child(3){
      flex-shrink:2;
      }
   ```
   로 1:3:2입니다. 1+3+2 = 6. 총 300px만큼 빼줘야 하기 때문에 300/6=50px.   
   nth-child(1)은 50px 감소   
   nth-child(2)는 3`*`50px = 150px 감소   
   nth-child(3)은 2`*`50px = 100px 감소   
   가 됩니다.   

1. # flex-shrink를 0으로 설정하는 경우   
   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="NWVYZqR" data-pen-title="flex_shrink_zero" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/NWVYZqR">
   flex_shrink_zero</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>   
      
   .item1:nth-child(1)은 flex-shrink:0;으로 설정하므로서 container의 width 250px에 맞춰 줄어들지 않고 글자 길이 대로 전부 출력이 됩니다. 하지만 .item1:nth-child(2)는 flex-shrink의 기본값인 1에 따라 shrink가 적용되어 container의 가로 크기 250px에 맞춰 가로 길이가 줄어듭니다. 이처럼 가로 길이를 부모에 맞춰야 할 경우 flex-shrink를 설정하고 그렇지 않은 경우 flex-shrink:0;으로 설정해서 크기를 아이템의 글자 길이 그대로 유지를 합니다.   

1. # basis, grow, shrink 한번에 사용하기

   ```cs
      /* flex-grow, flex-shrink, flex-basis 순으로 작성 */

      flex: 1;
      /* flex-grow:1; flex-shrink:1; flex-basis:0; */

      flex: 1 1 auto;
      /* flex-grow:1; flex-shrink:1; flex-basis:auto; */

      flex: 1 500px;
      /* flex-grow:1; flex-shrink:1; flex-basis:500px; */
   ```   
   주의 할 점은 flex:1;인 경우 flex-basis는 0이 됩니다.   
   flex-grow는 Item들이 container의 크기에 비해 부족한 경우 더 늘여주고,   
   flex-shrink는 item들이 container의 크기에 비해 더 큰 경우 줄여서   
   container와 item들의 크기를 맞추게 됩니다.   

1. # flex-Item속성 : order
   flex item의 순서를 설정합니다. 기본값은 0이고, 숫자가 작을수록 먼저 왼쪽에 위치하게 됩니다.   

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="bGJQyBP" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/bGJQyBP">
   ch05.item_order</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

