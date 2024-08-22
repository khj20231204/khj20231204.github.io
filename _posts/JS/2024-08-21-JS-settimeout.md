---
layout: single
title: setTimeout과 재귀
categories: JS
tag: 
---

1. # setTimeout
   setTimeout(function, milliseconds) 지정한 function를 milliseconds 이후에 한 번 실행하는 함수입니다. setInterval(function, milliseconds)은 지정한 function를 milliseconds마다 실행하는 함수입니다. 하지만 재귀적으로 호출하게 되면 setTimeout함수도 milliseconds마다 실행되게 됩니다.   

	```html
		<div>
			<input type="text" class="clockText">
			<br>
			<button onclick="showDate()">시작</button> //showDate()함수를 호출
			<button onclick="stop">멈춤</button>
		</div>

		<script>
			function showDate(){
				var t = new Date();
				
				var y = t.getFullYear();	//연도
				var m = t.getMonth() + 1; 	//월(0 ~ 11)
				var d = t.getDate();	//일
				var allDate = y + "-" + m + "-" + d;
				
				//시 분 초는 뒤에 's'가 붙음
				var h = t.getHours();		//시간, 뒤에 s붙음
				var mm = t.getMinutes();	//분, 뒤에 s붙음
				var s = t.getSeconds();		//초, 뒤에 s붙음
				allDate += h + ":" + mm + ":" + s;
				
				//요일
				var w = t.getDay();
				allDate += " " + w + "-";	//일0 월1 화2 수3 목4 금5 토6
				var week = ["일요일","월요일","화요일","수요일","목요일","금요일","토요일"];
				allDate += week[w];
				
				var clock = document.querySelector(".clockText");
				clock.value = allDate;
				st = setTimeout("showDate()", 500); //<-------- 재귀로 setTimeout호출, st 전역변수에 setTimeout 할당
			}
		</script>
	```   
   showDate함수 안에서 setTimeou("showDate()", 500)로 자신을 재귀호출 했기 때문에 500 milliseconds 후 계속 해서 실행이 됩니다.   
   만약 setTimeout이 밖으로 빠져있다면 한번만 실행이 됩니다.   
   
	```html
		<div>
			<input type="text" class="clockText">
			<br>
			<button onclick="start()">시작</button>   //start()함수를 호출
			<button onclick="stop()">멈춤</button>
		</div>
		
		<script>
		function showDate(){
			var t = new Date();
			
			var y = t.getFullYear();	
			var m = t.getMonth() + 1; 
			var d = t.getDate();	
			var allDate = y + "-" + m + "-" + d;
			
			var h = t.getHours();		
			var mm = t.getMinutes();	
			var s = t.getSeconds();		
			allDate += h + ":" + mm + ":" + s;
			
			var w = t.getDay();
			allDate += " " + w + "-";
			var week = ["일요일","월요일","화요일","수요일","목요일","금요일","토요일"];
			allDate += week[w];
			
			var clock = document.querySelector(".clockText");
			clock.value = allDate;
		}
		
		function start(){
			st = setTimeout("showDate()", 500);     //setTimeout을 밖에서 실행합니다. 
		}
	```   
   setTimeout을 밖에서 실행하면 한번만 실행이됩니다.   
   <span style="color:red">*setTimeout과 이벤트에 함수를 할당시 ()괄호를 넣지 않으면 제대로 동작하지 않습니다.</span>   
	<span style="color:red">*setTimeout과 이벤트에 함수를 할당시 ""따옴표를 넣지 않으면 제대로 동작하지 않습니다.</span>   

1. # clearTimeout
   setTimeout의 실행을 멈추게 할 때 사용합니다. 재귀함수를 사용한 위에 소스의 경우 전역변수 w를 사용했기 때문에 외부 변수에도 호출이 가능합니다.   

	```javascript
		function stop(){
			clearTimeout(st);
		}
	```   
   전역변수로 선언한 st를 clearTimeout에 넣어서 setTimeout을 종료할 수 있습니다.   

1. # 전역변수
	```javascript
		var a;
		let a;
		const a;
		a;    //전역변수
	```   
   앞에 아무런 선언이 없으면 전역변수가 됩니다.   


