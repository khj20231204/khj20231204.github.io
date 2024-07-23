---
layout: single
title: (CSS)nth-child / nth-of-type
categories: CSS&HTML
tag: []
---

1. # nth-child와 nth-of-type
   nth-child는 해당 선택자의 부모 요소 안에서 모든 자식 요소 중에서 n번째 요소를 선택하는데 사용되는 CSS 선택자입니다. 이것은 요소의 순서에 따라 선택됩니다.   

   nth-of-type은 해당 선택자의 부모 요소 안에서 특정 유형의 요소 중에서 n번째 요소를 선택하는데 사용되는 CSS 선택자입니다. 이것은 요소의 유형에 따라 선택됩니다.   

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="abxJYvm" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/abxJYvm">
   nthchild_nthColn </a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

1. # nth-child(2)의 뜻

   fruit란 부모 클래스에 두번째 자식이 div이면 적용   
   <span style="color:red;font-style:bold">①</span>.fruit <span style="color:red;font-style:bold">③</span>div:<span style="color:red;font-style:bold">②</span>nth-child(2)   

   인지 아니면   

   fruit란 부모 클래스에 div요소 중 두번째 자식에 적용   
   <span style="color:red;font-style:bold">①</span>.fruit <span style="color:red;font-style:bold">②</span>div:<span style="color:red;font-style:bold">③</span>nth-child(2)   

   인지 아니면
   fruit란 부모 클래스 전체 범위 안에서 모든 두번째 자식이 div이면 적용   

   인지 헷갈림   

   1)child(2)   
   두번째 자식이란 "호박3"이 해당합니다. 호박1과 호박2는 child가 아니라 자손(descendent)이 됩니다. `<span>딸기`와 `<div>호박3</div>`는 형제가 됩니다. .fruit의 child는 딸기, 호박3이 됩니다.   
   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="abxJYvm" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/abxJYvm">
   nthchild_nthColn </a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
      
   <br>      
   2)fruit클래스의 두번째 자식이 div이면 적용? 아니면 fruit클래스의 div 중 두번째 자식에 적용?   
   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="bGJqvYy" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/bGJqvYy">
   nth_child_2</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
   "두번째 자식이 div이면 적용"인 경우 호박1이 빨간색이 될테고, "div중 두번째 자식에 적용"이면 호박2에 빨간색이 됩니다.   
   호박1에 빨간색이 나타났기 때문에 "두번째 자식이 div이면 적용"이 됩니다.   

1. # nth-of-type(2)의 뜻
   div:nth-child(2)는 "두번째 자식이 div이면 적용"이 됩니다.   
   div:nth-of-type(2)은 "div 중 두번째 타입에 적용"이 됩니다.   

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="NWmpYwZ" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/NWmpYwZ">
   nth_child_2</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
      
   만약 div:nth-of-type(2)가 "두번째 타입이 div이면 적용"이라면 딸기 다음 호박1이나, 딸기 다음 호박3이 빨간색이 되어야 하지만 호박4가 빨간색이 되었습니다.   
   따라서, div 중 두번째 타입에 적용이 됩니다.   

1. # first-child
   first-child와 last-child가 적용되는데 있어서 다음 2가지 규칙이 있습니다.      
   1) __← 뒤에서 부터 해석!__   
   → 앞에서부터 해석하는 거 아님   
   2) __모든 경우 마다__ 첫번째 자식을 찾습니다.   
   3) __부모가 적용되면 자식들은 자동 적용__   

   div:first-child : 첫번째 자식이 div이면 해당(O) / div요소 중 첫번째 자식에 해당(X)   
   .parents:first-child : 첫번째 자식의 셀렉터가 .parents이면 해당 / 셀렉터가 parents 중 첫번째 자식에 해당(X)   
   여기 말하는 첫번째 자식이 적용되는 범위는 __모든 태그__ 에 해당됩니다.   

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="MWdQqWd" data-pen-title="first_child" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/MWdQqWd">
   first_child</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
   
   ```html
      <span>
         <span>만약 없으면</span>
      </span>

      <div> <!-- 위에 "만약 없으면" 태그가 없다면 body의 첫번째 div 여기 -->
         <span>여기가 적용</span> 
      </div>

      <br>

      <div>
         <span>
            <span id="1">
               <div>div_1</div> <!-- id="1"의 첫번째 자식으로서 적용 -->
            </span>
         </span>
      </div>

      <br>

      <div>
         <span>
            <span id="2">
               <span>span_1</span> <!-- 여기가 첫번째 자식 -->
               <div>div_2</div> <!-- id="2"의 두번째 자식이기 때문에 적용 안됨 -->
            </span>
         </span>
      </div>

      <br>

      <span id="3">
         <div>div_3</div> <!-- id="3"의 첫번째 자식으로 적용 됨 -->
         <span>span_2</span>
      </span>

      <br>

      <span id="4">
         <span>span_3</span>
         <div>div_4</div> <!-- id="4"의 두번째 자식으로 적용 안 됨 -->
      </span>

      <br>

      <span>
         <div id="here"> <!-- 여기서 첫번째 자식으로 해당 -->
            <span>
               <span>자식이면 다 적용1</span>
               <span><span>자식이면 다 적용2</span></span>
               <span><span><div>자식이면 다 적용3</div></span></span>
               <!-- id="here"인 부모가 적용 되었기 때문에 자식들은 전부 적용 -->
            </span>
            <span>span_4</span> <!-- 여기까지 적용 -->
         </div>
         <span>span_5</span> <!-- id="here"의 자식이 아니라서 적용 안됨 -->
      </span>
   ```   

1. # last-child
   위에 first-child와 마찬가지로 같은 조건을 가집니다.   

   ```html
      <div id="1">
         <span id="2">
            <div>div_1</div> <!-- id="2"의 마지막 자식으로 적용 -->
         </span>
         <div>div_2</div> <!-- id="1"의 마지막 자식으로 적용 -->
      </div>

      <br>

      <div id="3">
         <span id="4"><div>div_3</div></span> <!-- id="4"의 마지막 자식으로 적용 -->
         <div id="5"><span>div_4<span></div> <!--id="5"의 마지막 자식이지만 span이라서 적용 안됨 -->
         <div>div_5</div> <!-- id="3"의 마지막 자식으로 적용 -->
      </div>
               
      <br>
           
      <span>
         <div>div_6</div>
         <span id="6"><div>div_7</div></span>
         <!-- id="6"의 마지막 자식으로 적용 -->
         <div><span>div_8<span></div> <!-- div가 아니라서 적용 안됨 -->
         <span>div_9</span> <!-- div가 아니라서 적용 안 됨 -->
      </span>
   ```   

