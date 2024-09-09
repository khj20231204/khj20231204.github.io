---
layout: single
title: (CSS)셀렉터
categories: CSS&HTML
tag: []
---   

1. # 셀렉터
   셀렉터 유형   
   1)태그 이름   
   2)class 속성    
   3)id 속성   
   4)셀렉터 조합하기   
   5)가상 클래스 셀렉터   
   6)그 외 셀렉터   

1. # 태그 이름
   태그 이름을 셀렉터로 사용할 수 있습니다. 셀렉터와 같은 이름의 모든 태그에 스타일 시트가 적용됩니다. 태그 셀렉터는 ,(콤마)로 분리합니다.   

   ```css
      p {color : grey;}
      h1, h3 {color : red;}
   ```   

1. # class 속성
   셀렉터 이름 앞에 .(점)을 붙입니다. html태그들에 class 속성을 입력 후 스타일 시트를 적용할 수 있습니다.   

   ```html
   <head>
      <style>
         .myclass {color : blue;}
         div.myclass2 {color : green;}
      </style>
   </head>
   <body>
      <span class="myclass">안녕</span>
      <span class="myclass">반가워</span>

      <div class="myclass2">연습장</div>
      <p class="myclass2">에 연습</p>
   </body>
   ```   
   <head>
      <style>
         .myclass {color : blue;}
         div.myclass2 {color : green;}
      </style>
   </head>
   <body>
      <span class="myclass">안녕</span>
      <p class="myclass">반가워</p>

      <div class="myclass2">연습장</div>
      <p class="myclass2">에 연습</p>
   </body>   
   "myclass는 class값이 myclass인 모든 태그에 스타일을 적용합니다. 하지만 div.myclass2는 div태그 중 클래스가 myclass2인 태그에만 적용을 합니다.   

1. # id 속성
   셀렉터 이름 앞에 #(샵)을 붙입니다. class속성 값은 여러 태그에 같이 사용할 수 있지만 id속성 값은 하나의 태그에만 사용할 수 있습니다. id속성 셀렉터가 class속성 셀렉터보다 우선순위가 높습니다.   
   
   요점   
   1)id는 전체 페이지 중 하나의 요소에만 사용, class는 중복 사용 가능   
   2)id속성이 class속성 보다 우선순위가 높음   

   ```html
   <head>
      <style>
         #myid {color : blue;}
         div#myid2 {color : green;}
         #firstId {color: grey;}
         .secondClass {color : red}
      </style>
   </head>
   <body>
      <span id="myid">안녕</span>  
      <span id="myid">반가워</span>  <!-- 잘못된 사용 예 -->
      <p id="myid">또 다시</p> <!-- 잘못된 사용 예 -->

      <div id="myid2">연습장</div>

      <div id="firstId" class="secondClass">ID와 Class의 우선순위</div>
   </body>   
   ```   
   <head>
      <style>
         #myid {color : blue;}
         div#myid2 {color : green;}
         #firstId {color: grey;}
         .secondClass {color : red}
      </style>
   </head>
   <body>
      <span id="myid">안녕</span>  
      <span id="myid">반가워</span>  <!-- 잘못된 사용 예 -->
      <p id="myid">또 다시</p> <!-- 잘못된 사용 예 -->

      <div id="myid2">연습장</div>

      <div id="firstId" class="secondClass">ID와 Class의 우선순위</div>
   </body>   
      
   myid는 id이기 때문에 전체 페이지에서 1번 사용해야 합니다. id는 고유한 자신의 속성 한가지만 나타내기 때문입니다. 그렇기 때문에 "안녕"에 이미 myid가 사용되었기 때문에 "반가워"와 "또 다시"에서는 사용하지 않는 것이 좋습니다. span태그와 p태그에 myid 스타일 시트가 모두 적용은 되지만 잠재적 오류를 가지고 있기 때문에 id는 한 페이지에 하나의 요소에만 사용해야 합니다.   
   myid2처럼 한 요소에 한 개의 id가 와야 합니다.   
   id가 class보다 우선순위가 높기 때문에 "ID와 Class의 우선순위"가 해당 하는 요소에 firstId가 secondClass보다 스타일 시트가 먼저 적용이 되었습니다.   

1. # 고급 셀렉터
   1)연결 선택자 : 둘 이상의 선택자를 연결해서 적용될 요소 지정      
   2)가장 클래스와 가상 요소   
   가상 클래스는 클래스 이름 앞에 콜론(:)을 1개만 붙여 표시하는 방식   
   가상 요소는 클래스 앞에 콜론을 2개(::)를 붙여 표시하는 방식   

1. # 연결 선택자  
   - 자식 셀렉터   
   부모와 자식 관계에 있는 두 셀렉터를 > 로 조합한 관계입니다. 부모 바로 아래에 있는 요소가 해당 됩니다.   

   - 자손 셀렉터   
   부모와 자손의 관계는 부모와 자손을 나란히 나열하면 됩니다. 부모 아래에 있는 모든 셀렉터에 해당 됩니다.   

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="YzMNabg" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/YzMNabg">
   Untitled</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
      
   첫번째가 div의 자식이 되고, 두번째와 세번째는 div의 자손이 되므로 div style1로 자손들에 스타일 시트를 먼저 적용 후 "div > style1"로 자식에게만 적용하여 "첫번째" 요소만 빨간색이 되었습니다.   
   두번째, 세번째, 네번째가 전부 파란색 글씨가 적용되었습니다. 깊이는 상관없이 자식들은 그 이하의 모든 요소들이 포함됩니다.   

1. # 인접 형제 선택자와 형제 선택자   
   형제 요소 중에서 첫 번째 동생 요소만 선택하는 것을 __인접 형제 선택자__ 라고 합니다. 요소1과 요소2 사이에 '+' 기호를 표시하니다.   
   ```cs
      h1 + p {color:blue;}
   ```   
   h1의 첫번째 형제가 p이면 적용   

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="GRbOrNL" data-pen-title="Untitled" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/GRbOrNL">
   Untitled</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

   h1 다음 바로 span이 왔기 때문에 color:red가 적용되었습니다. p 다음 h2가 아니라 div가 왔기 때문에 color:blue는 적용되지 않았습니다.   

   모든 형제 요소에 적용   
   인접 형제 선택자와는 달리 모든 형제 요소에 적용되는 경우를 __형제 선택자__ 라고 합니다. 요소1과 요소2 사이에 `~`를 사용합니다.   
   ```cs
      h1 ~ p {color:blue;}
   ```   

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="rNEYjdY" data-pen-title="sibling2_selector" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/rNEYjdY">
   sibling2_selector</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

1. # 가상 클래스 셀렉터   
   사용자가 웹 요소를 클릭하거나 마우스 포인터를 올려놓는 등 특정 동작을 할 때 스타일이 바뀌도록 만들 때 사용합니다.

      <table>
         <tr>
            <th>유형</th>
            <th>셀렉터</th>
            <th>설명</th>
         </tr>
         <tr>
            <td>마우스</td>
            <td>:hover</td>
            <td>마우스가 올라갈 때 스타일 적용</td>
         </tr>
         <tr>
            <td>마우스</td>
            <td>:active</td>
            <td>마우스로 누르고 있는 상황에서 스타일 적용</td>
         </tr>
         <tr>
            <td>폼 요소</td>
            <td>:focus</td>
            <td>폼 요소가 키보드나 마우스로 포커스를 받을 때 스타일 적용td>
         </tr>
         <tr>
            <td>링크</td>
            <td>:link</td>
            <td>방문하지 않은 링크에 스타일 적용</td>
         </tr>
         <tr>
            <td>링크</td>
            <td>:visited</td>
            <td>방문한 링크에 스타일 적용</td>
         </tr>
         <tr>
            <td>블록</td>
            <td>:first-letter</td>
            <td>p,div같은 블록형 태그의 첫 글자에 스타일 적용, span과 같은 인라인 태그에 적용되지 않음</td>
         </tr>
         <tr>
            <td>블록</td>
            <td>:first-line</td>
            <td>p,div같은 블록형 태그의 첫 라인에 스타일 적용</td>
         </tr>
         <tr>
            <td>구조</td>
            <td>:nth-child(even)</td>
            <td>짝수번째 모든 자식 태그에 스타일 적용</td>
         </tr>
         <tr>
            <td>구조</td>
            <td>:nth-child(1)</td>
            <td>첫 번째 자식 태그에 스타일 적용</td>
         </tr>
      </table>
      
   예제1)   
   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="LYvWdPW" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/LYvWdPW">
   ch04.selecter_pseudoClass</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
      
   예제2)   
   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="qBzVRQQ" data-pen-title="navi" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/qBzVRQQ">
   navi</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

1. # 그 외 셀렉터   
   1)전체 셀렉터   
   와일드카드 문자(*)를 사용하면 웹 페이지의 모든 html에 스타일 시트가 적용됩니다.   
   
      `*` {color : green;}
   
   페이지의 모든 글자색이 그린색이 됩니다.   

   2)속성 셀렉터   
   html태그의 속성에 값이 일치하는 경우에만 적용되는 스타일 시트입니다.   
   ```css
      input[type="text"] {color : red;}
   ```   
   input타입이 text인 모든 태그에 적용되는 셀렉터입니다.   


   
