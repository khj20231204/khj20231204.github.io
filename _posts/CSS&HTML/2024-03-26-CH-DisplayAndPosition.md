---
layout: single
title: (CSS)display와 position
categories: CSS&HTML
tag: []
---

1. # 배치
   HTML 태그가 출력되는 위치를 지정하는 것을 배치라고 합니다.   

   배치와 관련된 프로퍼티   
   - display   
   - position   
   - left, right, top, bottom   
   - float   
   - z-index   
   - visibility   
   - overflow   

1. # 블록 박스와 인라인 박스
   블록 태그 - `<p>, <div>, <h1>, <ul>`   
   인라인 태그 - `<a>, <span>, <img>`   

   블록 태그는 블록 박스로, 인라인 태그는 인라인 박스로 다룹니다.

1. # 박스 유형 제어 display
   display 프로퍼티를 이용하면 디폴트 박스 유형인 블록 박스와 인라인 박스 유형을 달리 지정할 수 있습니다. CSS3 박스 유형은 3가지이며 display 프로퍼티를 이용하여 지정할 수 있습니다.   

   - 블록 박스 - display:block   
   - 인라인 박스 - display:inline   
   - 인라인 블록 박스 - display:inline-block   
   - 플렉스 박스 - display:flex   

   |블록박스<br>(display:block)|인라인 박스<br>(display:inline)|인라인 블록 박스<br>(display:inline-block)|
   |:----------------------------:|:------------------------:|:--------------------------:|
   |     블록박스 안에서만 위치    |    모든 박스 안에서 위치   |    모든 박스 안에서 위치    |
   |      항상 새라인에서 시작     |    새 라인에서 시작 못함   |    새 라인에서 시작 못함    |
   |   옆에 다른 요소 배치 불가능  |  옆에 다른 요소 배치 가능  |   옆에 다른 요소 배치 가능  |
   |    height, width 조절 가능   | height, width 조절 불가능 |   height, width 조절 가능  |
   |padding, border, maring 조절 가능|padding, border, maring 조절 불가능|padding, border, maring 조절 가능|

1. # block 박스
   폭의 길이와 무관하게 반드시 한 줄을 꽉 채우게됩니다.   
   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="BaEJXoR" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/BaEJXoR">
   ch05.01_blockBox</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
   블록요소는 없는 여백도 만들어서 가로를 가득 채우게됩니다.   

1. # inline 박스
   인라인은 요소의 폭과 높이가 요소 내용과 도일하게 고정됩니다. 추가적이 여백도 없고, 폭과 높이가 텍스트에 딱 맞춰집니다. 단, __weight와 height 속성이 적용되지 않습니다.__   
   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="dyLJxMP" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/dyLJxMP">
   ch05.01_inlineBox</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

1. # inline-block 박스
   가로로 여러 요소를 배치할 수 있으면서 width와 height를 설정할 수 있습니다.   
   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="BaEJXpd" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/BaEJXpd">
   ch05.01_inline-blockBox</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
      
1. # 박스의 배치 position
   브라우저는 웹 페이지에 나타난 순서대로 html태그를 배치합니다. 이를 normal flow라고 합니다. position 프로퍼티를 이용하면 normal flow를 무시하고 원하는 위치에 박스를 배치시킬 수 있습니다.   

   - 정적 배치 : position - static(디폴트)   
   - 상대 배치 : position - relative   
   - 절대 배치 : position - absolute   
   - 고정 배치 : position - fixed   
   - 유동 배치 : float:left 혹은 float:right   

   각각의 배치에 따라 다른 height, width, top, bottom, left, right가 적용됩니다.   

1. # 정적 배치 - static
   웹 페이지가 작성된 순서대로 html 태그의 출력 위치를 정하는 기본 방식.    
   position:static에서는 작성된 순서대로 출력되기 때문에 top, bottom, left, right는 영향을 주지 않습니다.   

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="rNbGBvd" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/rNbGBvd">
   ch05.01_static</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>   

   <br>
      
1. # 상대 배치 - relative
   position:relative를 사용하게 되면 순서대로 작성된 normal flow에 의해 위치된 __현재 위치__ 에서 top, bottom, left, right 프로퍼티 값만큼 이동한 상대 위치에 배치되게 됩니다.   

   top와 bottom이 동시에 적용되면 bottom이 무시되고, left와 right가 동시에 적용되면 right가 무시됩니다.   

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="VwNMZNZ" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/VwNMZNZ">
   ch05.01_relative</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>   
   
   <br>
      
1. # 절대 배치 - absolute
   position:absolute를 하게 되면 __부모 태그 안에서__ 상대 좌표로 이동하게 됩니다. 부모 태그를 기준으로 top, left, bottom, right 에 위치하게 됩니다. 브라우저 크기가 변해도 태그 위치는 변하지 않습니다.

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="vYMerqB" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/vYMerqB">
   ch05.01_absolute</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

   absoluteCss1~absoluteCss5까지 모두 total를 기준으로 top, left, bottom, right가 정해집니다.   

   ```css
      .total{
         background-color:orange;
         position:relative; /*전체 div를 이동*/
         top:60px;
         left:80px;
      }
   ```   
   전체 div를 이동 시키기 위해서 현재위치를 기준으로 top으로 60px, left로 80px를 이동하게 됩니다.   

   ```css
      .absoluteCss1{
         position:absolute; 
         /*absolute를 하고 top과 left를 설정 안 했기 때문에
         기본값 top:0px, left:0px가 됨*/
      }
   ```   
   absolute를 하게 되면 현재 이동한 전체div total을 기준으로 이동하게 되는데 top, left, bottom, right를 설정하지 않았기 때문에 top:0px, left:0px, bottom:0px, right:0px가 되어서 div1,div2가 겹쳐지게 됩니다.   

   absoluteCss3과 absoluteCss5는 position:absolute로 기준이 __부모div 태그를 기준__ 으로 이동했기 때문에 겹쳐지게 되는데, absolute4는 position:relative로 __기존 div4가 있던 위치를 기준__ 으로 top:180px, left:200px 이동 했기 때문에 div3, div5와 겹쳐지지 않습니다.

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="VwNMEdR" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/VwNMEdR">
   ch05.01_parent_absolute</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

1. # 고정 배치 - fixed
   스크롤하거나 브라우저 크기를 변경해도 뷰포트(브라우저 윈도우)의 일정 위치에 항상 고정시킬 때 사용합니다.  절대 배치는 부모 태그를 기준으로 고정된 위치에 나타나게 되고, 고정 배치는 뷰포트를 기준으로 고정된 위치에 나타나게 됩니다.   

