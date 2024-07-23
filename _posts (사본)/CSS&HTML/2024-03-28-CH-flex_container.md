---
layout: single
title: (CSS)배치(flex_container)
categories: CSS&HTML
tag: []
---
      

1. # flex 박스
   인라인 블록 요소의 사용을 더욱 편하게 하기 위해 설계되었습다. 블록 요소가 마치 인라인처럼 텍스트의 크기만큼 폭을 차지하게 됩니다. block, inline, inline-block과는 다르게 부모 태그에 flex를 설정하면 속성 값에 따라 자식 요소들이 정렬이 됩니다.   
   flex의 부모 태그를 Flex Container라 하고, 자식 태그를 Flex Item이라 합니다. 각각 적용되는 속성이 따로 존재하며 다음과 같습니다.   
   
   __부모 태그 : Flex Container__ 의 속성들   
   display, flex-flow, flex-direction, flex-wrap   
   justify-content, align-content, align-items   

   __자식 태그 : Flex Item__ 의 속성들   
   order, flex, flex-grown, flex-shrink, flex-basis, align-self   

   flex를 사용하기 위해서는 부모 태그를 Flex Container로 만들어야 하는데 그 방법이 부모 태그에 displady:flex를 적는 것.   
   부모 컨테이너에서만 display:flex를 선업합니다.

   - display:flex => __블록 요소__ 처럼 Flext Container를 구성   
   - display:inline-flex => __인라인 요소__ 처럼 Flex Container를 구성   
   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="mdgXpLR" data-pen-title="ch05.01_flex_inlineFlex" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/mdgXpLR">
   ch05.01_flex_inlineFlex</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>     
   flex는 자식 아이템 사이 정렬은 수평 정렬이 되고 부모 컨테이너와 다른 태그와의 관계가 블록입니다.   
   flex_Item1 사이는 수평 정렬이 되고, 다른 태그 사이는 블록으로 구성이 되어 flex_Item1과 flex_Item2가 줄바꿈이 됩니다.   
   반면, inline-flex는 자식 아이템 사이 정렬도 수평 정렬이 되고, 부모 컨테이너와 다른 태그와의 관계도 인라인으로 수평 정렬이 됩니다.   
   inline_Item1 사이도 인라인처럼 수평 정렬이 되었고, inline_Item2과도 인라인처럼 수평 정렬이 됩니다.   
   즉, flex는 자식 아이템 사이 정렬은 인라인으로 수평 정렬 가능, 부모 컨테이너와 다른 태그 사이 정렬은 블록으로 줄바꿈.
   inline-flex는 자식 아이템 사이 정렬도 인라인으로 수평 정렬 가능, 부모 컨터이너와 다른 태그 사이 정렬도 인라인으로 수평 정렬 가능.

   inline-flex와 inline-block은 다른 태그들과 관계에서 인라인으로 구성되어 장문의 글이 수평으로 옆에 배치가 됩니다.  
   두 개가 비슷한데 차이점은.. ... ... 찾아봐야 되겠습니다.

1. # flex Container속성 : flex-direction
   __플렉스 아이템__ 을 정렬할 주 축을 설정. 플렉스는 기본적으로 플렉스 아이템들을 가로로 설정합니다. 하지만 flex Container의 속성으로 flex-direction을 주면 가로 외의 방향으로 아이템들을 설정할 수 있습니다.   

   __행 - 수평__   
   row : 행축(좌 → 우), 수평 정렬을 왼쪽에서 시작, <u>기본값</u>   
   row-reverse : 행축(우 → 좌), 수평 정렬을 오른쪽에서 시작   
   Main-axis가 가로 축  
   *플렉스는 기본값이 가로 정렬이기 때문에 명시적으로 row을 사용하는 경우는 드물다

   __열 - 수직__   
   column : 열축(위 → 아래), 수직 정렬을 위에서 시작      
   column-reverse : 열축(아래 → 위), 수직 정렬을 아래에서 시작   
   Main-axis가 세로 축   

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="VwNxQbj" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/VwNxQbj">
   ch01.flex_direction</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

1. # flex Container속성 : flex-wrap
   공간이 줄어들 경우 플렉스 아이템의 줄 바꿈 여부를 설정, 부모 컨테이너의 크기보다 자식 아이템들이 더 클 경우 자식 아이템들이 부모 컨테이너를 삐져나오게 되는데(nowrap으로 기본 값) 이 때 삐져나오는 것을 없애기 위해 아래로 떨어뜨리는 것이 wrap기능.

   nowrap : 줄 바꿈 없음, <u>기본값</u>   
   wrap : 크기를 유지하며 아래로 떨어뜨린다.   

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="OJGZrBX" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/OJGZrBX">
   Untitled</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
   
   <br>

   <img src="../../imgs/CH/flex_wrap_normal.png" style="border:3px solid black;border-radius:9px;width:700px">   
   공간이 허용될 땐 전부 가로 100px, 세로 100px 공간을 가진 정사각형의 모양입니다.   
   하지만 공간이 줄어들 경우 nowrap인 경우   
   <img src="../../imgs/CH/flex_nowrap.png" style="border:3px solid black;border-radius:9px;width:460px">   
   작은 공간에 줄바꿈없이 전부 넣게 되고 그 결과 정사각형이 찌그러지게 됩니다.   
   wrap의 경우는   
   <img src="../../imgs/CH/flex_wrap.png" style="border:3px solid black;border-radius:9px;width:460px">   
   자동 줄 바꿈이 되어서 가로 100px, 세로 100px의 정사각형을 그대로 유지하게 됩니다.   

   wrap을 준 상태에서 item에 height를 주지 않으면 item의 높이는 auto가 되고 auto는 부모인 container의 높이를 따라갑니다. 이때, 아이템의 기본 설정이 strech이므로 다음과 같이 container의 전체 크기 300px에 맞춰 길쭉하게 늘어난 형태를 가진다   
   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="oNOQoMN" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/oNOQoMN">
   ch05_flex_strech_height</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

1. # flex Container속성 : flex-flow
   flex-direction과 flex-wrap을 한꺼번에 지정할 수 있는 단축 속성입니다. flex-direction과 flex-wrap 순으로 한 칸 떼고 써주시면 됩니다.   

   ```s
      .container {
         flex-flow : row wrap;

         # 아래 두 줄을 줄여 쓴 것 입니다.
         /* flex-direction : row; */
         /* flex-wrap : wrap; */
      }

   ```

1. # flex Container속성 : justify-content(정렬)
   "justify"는 메인축(오뎅꼬치) 방향으로 정렬   
   "align"은 수직축(오뎅을 뜯어내는) 방향으로 정렬   
   __기본 축__ 을 따라 나열되어 있는 플렉스 아이템들의 나열 방식   

   direction:row -> 주축은 가로   
   <img src="../../imgs/CH/flex_row_order.png" style="border:3px solid black;border-radius:9px;width:400px">   
   아이템들이 빨간색 타원의 위치로 정렬됩니다.   

   direction:column -> 주축은 세로   
   <img src="../../imgs/CH/flex_column_order.png" style="border:3px solid black;border-radius:9px;width:400px">   
   아이템들이 빨간색 타원의 위치로 정렬됩니다.   

   <p class="codepen" data-height="600" data-default-tab="html,result" data-slug-hash="oNOyyab" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/oNOyyab">
   ch05.flex_justify_direction</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

   direction:row로 했을 경우 주축이 가로가 됩니다.   
   justify-contents:flex-start는 가장 왼쪽   
   justify-contents:center는 가운데   
   justify-contents:flex-end는 가장 오른쪽에 위치가 됩니다.   

   direction:column인 경우 주축이 세로가 됩니다.   
   justify-contents:flex-start는 세로 축을 기준으로 가장 윗쪽에 위치   
   justify-contents:center는 가운데   
   justify-contents:flex-end는 가장 아랫쪽에 위치합니다.   


1. # flex Container속성 : justify-content(공간 삽입)
   __direction:row방향으로 설명__   

   아이템들 사이에 공간을 주는 속성으로   
   justify-contents:space-between;   
   justify-content:space-around;   
   justify-content:space-evenly;   
   <span style="color:red">*space-evenly의 경우 MS계열의 브라우저(익스플러로, 엣지)의 경우 지원이 되지 않기 때문에 따로 처리를 해야 합니다</span>   
   가 있습니다.   

   <img src="../../imgs/CH/space_between.png" style="border:3px solid black;border-radius:9px;width:800px">    
   space-between

   <img src="../../imgs/CH/space_around.png" style="border:3px solid black;border-radius:9px;width:800px">    
   space-around

   <img src="../../imgs/CH/space_between_around.png" style="border:3px solid black;border-radius:9px;width:800px">    
   space-between과 space-around의 차이

   <img src="../../imgs/CH/space_evenly.png" style="border:3px solid black;border-radius:9px;width:800px">    
   space-evenly   

   <img src="../../imgs/CH/space_around_evenly.png" style="border:3px solid black;border-radius:9px;width:800px">    
   space-around와 space-evenyl이 차이   

1. # flex-Container속성 : align-items
   플렉스 박스의 교차 축 설정. 주축에서 + 모양으로 그렸을 때 교차되는 축이 교차 축의 기준으로 item들이 이 __교차 축을 기준__ 으로 위치하게 돕니다.   
   
   align-content와 다르게 한 줄의 아이템당 부모container의 높이에 맞춰 각 줄에 정렬이 됩니다.
   <img src="../../imgs/CH/align_items.png" style="border:3px solid black;border-radius:9px;width:800px">   
   
   display:flex   
   => ㅡ 가로 축이 기준 축으로 교차 축은 |   
   align-items:flex-start 세로 축을 기준으로 가장 윗쪽에 위치   
   align-items:center 가운데   
   align-items:flex-end 가장 아랫쪽에 위치

   display:flex;   
   flex-direction:column;   
   => | 세로 축이 기준 축으로 교차 축은 ㅡ   
   align-items:flex-start 가로 축을 기준으로 가장 왼쪽에 위치   
   align-items:center 가운데   
   align-items:flex-end 가장 오른쪽에 위치 

   <p class="codepen" data-height="600" data-default-tab="html,result" data-slug-hash="NWmEXaO" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/NWmEXaO">
   align_items</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

   ```css
      .row_flex_start{
      background-color:royalblue;
      display:flex;  /* 기준 축은 ㅡ*/
      /*   
      flex-direction:row; 
      display:flex 기본값이 row라 생략가능  
      */
      align-items:flex-start;  /* 교차 축 | 를 기준으로 윗쪽에 위치*/
      flex-wrap:wrap;  /* 공간이 부족하면 기존 모양을 유지하면서 줄 바꿈 */
      height:500px;
      width:200px;
      }

      .column_flex_start{
      background-color:royalblue;
      display:flex;  /* 기준 축은 ㅡ */
      flex-direction:column;  /* 기준 축을 | 로 바꿈*/
      align-items:flex-start;  /* 아이템들을 교차 축 ㅡ를 기준으로 앞쪽에 위치*/
      height:400px;
      width:500px;
      }
   ```

1. # flex-Container속성 : align-content
   align-items가 교차 축으로 한 줄만 정렬하는 방식이라면, align-content는 교차 축으로 여러 줄을 정렬하는 방식입니다. 보통 align-content보다 align-items를 더 많이 사용합니다.   

   items와 속성은 같습니다. 단, 자식 아이템들이 여러 줄 겹쳐져서 정렬이 됩니다.   
   display:flex   
   => ㅡ 가로 축이 기준 축으로 교차 축은 |   
   align-content:flex-start 세로 축을 기준으로 가장 윗쪽에 위치   
   align-content:center 가운데   
   align-content:flex-end 가장 아랫쪽에 위치

   display:flex;   
   flex-direction:column;   
   => | 세로 축이 기준 축으로 교차 축은 ㅡ   
   align-content:flex-start 가로 축을 기준으로 가장 왼쪽에 위치   
   align-content:center 가운데   
   align-content:flex-end 가장 오른쪽에 위치 

   <p class="codepen" data-height="600" data-default-tab="html,result" data-slug-hash="mdgQpGx" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/mdgQpGx">
   align_content</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>


1. # 정렬 간단히 정리
   justify-content   
   <img src="../../imgs/CH/justify_content_shot.jpg" style="border:3px solid black;border-radius:9px;width:800px">   

   align-items   
   <img src="../../imgs/CH/align_items_shot.jpg" style="border:3px solid black;border-radius:9px;width:800px">   

   align-content   
   <img src="../../imgs/CH/align_content_shot.jpg" style="border:3px solid black;border-radius:9px;width:800px">   

   justify와 align은 flex-start, center, flex-end가 될 때 justify는 기본 가로 방향으로 이동, align은 기본 세로 방향으로 이동합니다.   
   justify가 기본 가로 방향으로 이동하는 경우는 flex-direction이 row일 때 기본 가로 방향으로 이동을 합니다. column이 되면 세로 방향으로 이동하게 됩니다.   
   align이 기본 세로 방향으로 이동하는 경우는 flex-direction이 row일 때 기본 세로 방향으로 이동을 합니다. column이 되면 가로 방향으로 이동하게 됩니다.   
   그리고, row와 column은 container에 속하는 items의 위치를 설정합니다. 각 item들을 꽂은 꼬치의 막대기 방향이라고 생각할 수 있습니다.   
   row는 item들을 가로 방향으로 꽂고, column은 item들을 세로 방향으로 꽂습니다.   
   <img src="../../imgs/CH/justify_align_explain.jpg" style="border:3px solid black;border-radius:9px;width:800px">   
   justify와 align은 item들이 기본 이동 방향.   
   flex-direction의 row와 column은 이동 방향 설정과 item들의 위치 설정.   

1. # 태그 가운데 정렬 방법
   ```s
      justify-content:center   
      align-items:center
   ```
   를 하게 되면 원하는 태그를 가운데 정렬할 수 있습니다.   

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="BaeJXXB" data-pen-title="flex_justify_align" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/BaeJXXB">
   flex_justify_align</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
