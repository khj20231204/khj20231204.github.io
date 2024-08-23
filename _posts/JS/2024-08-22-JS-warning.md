---
layout: single
title: 주의 사항
categories: JS
tag: []
---
 
1. # document.getElementById 위치
   ```html
      <body>
         <input type="text" id="name" onkeyup="keyup()"> 
         
         <script>
            var name = document.getElementById("name");     //keyup()함수 외부에 name을 선언
            
            function keyup(){
               var name = document.getElementById("name");  //keyup()함수 내부에 name을 선언
            }
         </script>
      </body>
   ```   
   `<script>`태그가 `<body>` 내부의 모든 태그 이후에 오더라도 keyup()함수 외부에서 name값을 가져온 경우 제대로 작동하지 않을 수 있습니다. input type="text" 이후에 만들어지는 onkeyup 이벤트 함수 내부에서 name값을 가져와야 제대로 동작합니다.   

1. # button의 기본값은 submit 내장
   ```js
      <form name="frm" method="post" action="send.jsp">
         <input type="button" value="버튼으로 동작">   //일반 버튼으로 작용
         <button>default submit</button>              //submit으로 작용
         <button type="button">버튼으로 동작</button>  //일반 버튼으로 작용
      </form>
   ```   
   `<input type="button">` 은 일반 버튼으로 작동합니다. `<button>`타입의 기본값은 submit이기 때문에 type을 정하지 않은 button은 submit으로 작동합니다. `<button type="button">`은 type를 button으로 정해줬기 때문에 일반 버튼으로 작동합니다.   

1. # form에서 submit
   ```html
     	<form id="frm" method="post" action="send.jsp" onsubmit="return button_submit()"> <!-- form에 submit이벤트를 등록, button_submit()함수의 리턴값을 받음 -->
         <input type="button" value="input type=button" onclick="input_submit()">
         <br>
         <input type="submit" value="input type=submit">
         <br>
         <button type="button" onclick="input_submit()">button type=button</button> <!-- onclick="button_submit()" 이벤트가 있으면 안된다 -->
         <br>
         <button>button</button>
      </form>

      <script>
         function input_submit(){
            
            if(조건을 만족하지 않으면)
               return false;
            
            frm.submit();  //일반 버튼에 적용
         }

         function button_submit(){
             if(조건을 만족하지 않으면)
               return false;

               //submit버튼에는 frm.submit()이벤트가 없다
		   }
      </script>
   ```   
   `<input type="button">`과 `<button type="button">` 은 일반 버튼으로 작용하기 때문에 input_submit()에서 조건을 만족하지 않으면 __return false__ 로 __함수를 종료__ 하고 frm에 submit()이벤트를 호출합니다. 일반 버튼 => frm.submit(); 호출   
   `<input type="submit">`과 `<button>` 은 submit기능으로 작용을 합니다.  type을 정하지 않는 `<button>`은 기본 값으로 submit 기능을 가지고 있습니다. submit기능이 있는 버튼은 버튼 자체에 이벤트를 등록하는 것이 아니라 form 객체에 이벤트를 등록합니다. form 객체에 `onsubmit="return button_submit()"` 로 button_submit()함수의 반환값이 false가 아니면 submit을 실행합니다.   

1. # 숫자 정렬
   ```javascript
      <script>
         var intArr = new Array(23,1,54,6,7,46,13);
         
         intArr.sort();
         console.log(intArr); //[1, 13, 23, 46, 54, 6, 7]
         intArr.forEach(i => console.log(i));
      </script>
   ```   
   intArr 숫자 배열을 sort() 함수로 정렬을 해줬는데 결과가 [1, 13, 23, 46, 54, 6, 7] 이란 정렬 결과를 가져왔습니다. 이유는 intArr배열의 구성원소 값들을 숫자가 아니라 문자로 인식하기 때문입니다. 그렇기 때문에 앞자리 숫자로만 오름차순 정렬하기 때문에 1,1,2,4,5,6,7 앞자리만으로 정렬이 되기 때문입니다. intArr배열의 sort함수를 수정해야 합니다.   

   ```javascript
      <script>
         intArr.sort((a,b) => a-b);
		   console.log(intArr); //[1, 6, 7, 13, 23, 46, 54]
      </script>
   ```   
   sort의 매개변수에 화살표 함수로 a와 b의 대소비교를 해줘야합니다.   

   (a, b) => a - b:   
   이 부분이 바로 비교 함수입니다.   
   a와 b는 배열에서 비교될 두 개의 숫자를 나타냅니다.   
   a - b는 두 숫자의 차를 계산합니다.   
   비교 함수는 다음과 같은 규칙을 따릅니다.   
   a - b가 음수이면 a가 b보다 작으므로, a를 앞에 두고 b를 뒤에 둡니다.   
   a - b가 양수이면 a가 b보다 크므로, b를 앞에 두고 a를 뒤에 둡니다.   
   a - b가 0이면 a와 b가 같으므로, 순서를 바꾸지 않습니다.   


