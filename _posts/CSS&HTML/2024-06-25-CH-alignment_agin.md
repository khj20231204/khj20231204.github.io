---
layout: single
title: (CSS)정렬
categories: CSS&HTML
tag: []
---

1. # 뷰포트를 기준으로 가로 가운데 정렬
   
   1)방법
   ```cs
      .content1 {
         background-color:gray;
         margin: 0 auto;
      }

      .content2 {
         background-color:gray;
         margin: 0 auto;
         width: 500px;
      }
   ```   
   를해야 하는데, margin: 0 auto를 사용하기 위해서 __width를 설정__ 해야 합니다.   

   위에 텍스트가 content1이 적용, 아래 텍스트가 cotent2가 적용되었습니다.   
   content1은 width가 없기 때문에 그냥 길게 글자가 나열되었고, content2는 가운데 정렬이 되었습니다.   
   <img src="../../imgs/CH/align_margin.png" style="border:3px solid black;border-radius:9px;width:600px">   




1. # 뷰토트를 기준으로 센터 정렬

1. # 부모 기준으로 가로 가운데 정렬

1. # 부모 기준으로 센터 정렬

1. # 자신의 텍스트를 가로 가운데 정렬

1. # 자신의 텍스트를 센터 정렬




1. # 가로 정렬
   ul li를 사용할 때 세로 정렬이 기본이 되는데 가로 정렬을 하는 방법입니다.   

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="OJezvLB" data-pen-title="ul_li_align" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/OJezvLB">
   ul_li_align</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

   ```cs
      .div1 {
         overflow: hidden;
         /* float를 사용할 때 부모 태그에 사용하면 이후에 오는 태그들은 레이아웃이 깨지지 않고 정렬이 됨 */
      }

      .div1 ul li {
         float : left;
         list-style-type: none; /* li 앞에 점 없애기 */
         padding : 5px;
         margin-bottom: 20px;
      }

      .div2 ul li {
         display: inline-block;
      }
   ```   

   가로 정렬하는 방법으로 float와 display를 inline-block으로 설정하는 방법이 있습니다.   
   div1에 float를 사용했습니다. float을 사용하게되면 해당 태그가 붕~ 떠서 정렬이 되기 때문에 전체 레이아웃이 깨질 수 있습니다. 이때 빈 공간을 채워서 레이아웃이 깨지지 않게 만들기 위해서 부모 태그에 `overflow: hidden`을 사용합니다.   
   div2에는 display: inline-block를 사용했습니다. inline-block을 사용하게 되면 inline과 block의 특징을 동시에 가지게 됩니다. inline의 특성으로 서로 붙어서 정렬이 되는 가로정렬이 되고 block처럼 넓이와 높이 size를 지정할 수 있습니다.   

1. # overflow

   overflow:hidden을 사용하면 float 요소 아래에 있는 태그들이 정렬되는 이유   

   부모 컨테이너의 높이 고정: overflow:hidden은 부모 컨테이너의 높이를 고정시켜, float 요소가 차지하는 공간을 포함하도록 합니다.   
   정확한 레이아웃 계산: 고정된 부모 컨테이너의 높이를 기반으로 브라우저는 나머지 요소들의 위치를 정확하게 계산할 수 있습니다.   
   float 요소의 영향 최소화: overflow:hidden은 float 요소가 다른 요소들의 레이아웃에 미치는 영향을 최소화합니다.   

   overflow:hidden을 float 요소의 부모에 적용하면, 부모 컨테이너의 높이가 고정되어 float 요소가 다른 요소들의 레이아웃에 미치는 영향을 최소화하고, 결과적으로 더욱 안정적인 레이아웃을 구축할 수 있습니다. 하지만 모든 경우에 overflow:hidden이 정답은 아니며, 레이아웃의 복잡성에 따라 다른 방법(flexbox, grid 등)을 사용해야 할 수도 있습니다.

