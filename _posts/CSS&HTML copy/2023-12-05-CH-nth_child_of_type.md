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
   <span style="color:red;font-style:bold">①</span>.fruit <span style="color:red;font-style:bold">②</span>bb:<span style="color:red;font-style:bold">③</span>nth-child(2)   

   인지 아니면
   fruit란 부모 클래스 전체 범위 안에서 모든 두번째 자식이 div이면 적용   

   인지 헷갈림   

   1)child(2)   
   두번째 자식이란 "호박3"이 해당합니다. 호박1과 호박2는 child가 아니라 자손(descendent)가 됩니다. `<span>딸기`와 `<div>호박3</div>`는 형제가 됩니다. .fruit의 child는 딸기, 호박이 됩니다.   
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
