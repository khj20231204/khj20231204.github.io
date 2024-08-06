---
layout: single
title: 실행 컨텍스트
categories: JS
tag: []
---
 
1. # 실행 컨텍스트
   context는 문맥, 맥락, 환경 정도로 해석할 수 있습니다. 코드에 영향을 주는 주변 코드나 변수들의 환경을 context라고 합니다. 코드의 배경이 되는 조건, 환경 정도를 뜻합니다. 코드를 실행하는데 필요한 배경이 되는 조건, 환경이 실행 컨텍스트입니다.   

   동일한 환경을 지닐 수 있는 조건   
   1)전역 공간 : 자바스크립트가 실행하면서부터 끝날 때까지 메모리를 차지   
   2)함수   
   3)eval : 불안요소라 제외   
   4)module : import되는 순간부터 실행되어 모듈 코드가 끝났을 때 컨텍스트 종료   
   메모리 공간을 실행하면서 차지하고 종료되면서 반납하는 방식이 결국 모두 함수의 개념과 같습니다. 동일한 환경이란 함수란 큰 의미 하나로 귀결됩니다.   
   전역 공간, 모듈, 함수로 묶인 내부에서는 결국 "같은 환경 안에 있다"라는 게 성립

   if/for/switch/while문은 
   블록스코프 개념이 도입됩니다. 반복문과 조건문 let과 const는 별개의 실행 컨텍스트를 만들지 않습니다.   

   자바스크립트는 오직 함수에 의해서만 컨텍스트를 구분할 수 있습니다.   
   따라서 컨텍스트란   
   ```
      함수를 실행할 때 필요한 조건, 환경정보를 담은 객체
   ```   
   가 됩니다.   

   ```js
      var a = 1;
      function outer(){
         console.log(a);

         function inner(){
            console.log(a);
            var a = 3;
         }

         inner();
         console.log(a);
      }

      outer();
   ```   
   1)전역공간 실행 컨텍스트가 열림   
   2)outer()함수 호출   
   3)inner()함수 호출   
   4)inner()함수 빠져나옴   
   5)outer()함수 빠져나옴   
   6)전연공간 빠져나옴   

   콜스택?   
   현재 어떤 함수가 동작중인지, 다음에 어떤 함수가 호출될 예정인지 등을 제어하는 자료구조   

   
1. # LexicalEnviroment

   실행 컨텍스트에는 세 가지 환경 정보가 있습니다.   
   VariableEnviroment : 식별자 정보 수집    
   LexicalEnviroment : 각 식별자의 '데이터' 추적   
   ThisBinding   
    
   VariableEnviroment는 오직 식별자 정보를 수집하는 용도로 사용됩니다. 컨텍스트 내부 코드들을 실행 하는 동안에 변화되는 값들은 LexicalEnviroment에 실시간으로 반영이 됩니다.   
   VariableEnviroment는 실시간 변화 반영X   
   LexicalEnviroment는 실시간 변화 반영O  
   VariableEnviroment와 LexicalEnviroment의 차이는 실시간 반영 여부만 있습니다.   

   __실행 컨텍스트가 실행을 하는데 필요한 환경정보를 담고 있는 것이 LexicalEnviroment입니다. LexicalEnviroment의 값에 따라 실행 컨텍스트가 실행이 됩니다.   

   LexicalEnviroment는 어휘적 환경, 사전적인 환경이라고 합니다.   
   
   |    영한 사전     |         실행 컨텍스트A 환경 사전      |
   |:---------------:|:------------------------------------:|
   |  able:할 수 있는 | 내부식별자a : 현재 값은 undefined이다 |
   |  apple:  사과   |      내부식별자b : 현재 값은 20이다    |
   |arrow:화살, 화살표|         외부 정보 : D를 참조한다      | 

   LexicalEnviroment   
   1)enviromentRecord : 현재 문맥의 식별자 정보 저장   
   2)outerEnviromentReference : 외부 문맥의 식별자 정보 저장    

1. # LexicalEnviroment예제
   ```js
      //중첩 함수일 때 LexicalEnviroment가 발생한다.
       function f(){
         var a = 22;
         function g(){
            console.log(a);
         }

         g(); //함수f 안에서 정의된 함수g
      }

     //------------------ 

      function h(){
         var a = 10;
         g();
      }

      function g(){
         console.log(a); //error발생
      }
   ```

1. # enviromentRecord
   현재 컨텍스트 식별자 정보를 수집해서 enviromentRecord에 담는 과정이 __호이스팅__ 입니다.   

   ```js
      console.log(a()); //a
      console.log(b()); //error 발생
      console.log(c()); //error 발생
      
      function a(){           //-------- 1)
         return 'a';
      }

      var b = function bb(){  //-------- 2)
         return 'b';
      }
      var c = function(){     //-------- 3)
         return 'c';
      }
   ```   
   1)의 함수만 전체가 끌어올려지고 2)와3)의 함수는 변수만 끌어올려집니다.   

   enviromentRecord에 끌어올려진 내용입니다.   
   ```
      {
         function a(){...},
         b : undefined,
         c : undefined
      }
   ```   
   함수정의로 선언된 1)만 함수 전체가 끌어올려지고 2),3) 함수 표현식으로 작성된 경우 할당된 참조변수만 끌어올려집니다.   

1. # outerEnviromentReference
   외부 환경 참조, 환경이란 LexicalEnviroment입니다. 현재 문맥에 관련있는 외부 식별자 정보를 참조한다는 뜻입니다.

   위의 예제에서 outer와 inner가 있는데 각각 LexcialEnviroment를 가지게 되고 LexcialEnviroment안에는 enviromentRecod, outerEnviromentReference가 있습니다.   
   ```cs   
      inner - LexcialEnviroment
         environmentRecord
         outerEnviromentReference

      outer - LexcialEnviroment  //inner함수의 outerEnviromentReference가 참조
         environmentRecord
         outerEnviromentReference

      전역 - LexicalEnviroment   //outer함수의 outerEnviromentReference가 참조
         environmentRecord
         outerEnviromentReference
   ```   
   inner함수의 outerEnviromentReference는 outer함수의 LexicalEnviroment를 참조하게 됩니다.   
   outer함수의 outerEnviromentReference는 전역의 LexcialEnviroment를 참조하게 됩니다.   

   outerEnviromentReference가 참조하는 게 __scope chain__ 이 됩니다. scope chain이 outerEnviromentReference가 의해서 만들어집니다. scope는 변수의 유효범위라는 뜻이고 이것은 outerEnviromentReference에 의해 결정되어집니다.      
   *scope : 변수의 유효범위   

   inner함수의 outerEnviromentReference는 outer의 LexcialEnviroment를 참조할 수 있지만 outer함수의 outerEnviromentReference는 inner함수의 LexcialEnviroment를 참조할 수 없습니다. 왜냐면 콜스택에 먼저 입력된 outer함수는 inner함수를 알 수 있는 어떤 정보도 없기 때문입니다. 이게 변수의 유효범위를 말하는 것이고 스코프입니다.   

   *shadowing   
   
1. # 소스 컨텍스트 저장 과정
   ```js
      var a = 1;
      function outer(){       //outer함수 정의
         console.log(a);      //---A

         function inner(){    //inner함수 정의
            console.log(a);   //---B
            var a = 3;
         }

         inner();             //inner함수 호출
         console.log(a);      //---C
      }

      outer();                //outer함수 호출
      console.log(a);   
   ```   
   1)전역 Excecution Context활성화    
   2)변수 a 선언(할당은 아님 a는 undefined)   
   3)함수 outer 선언   
   ------------------- 전역 context의 enviromentRecord 수집 끝   
   4)변수 a에 1할당   
   5)함수 outer 호출 → outer Excecution Context 활성화   
   6)"outer함수 호출"은 호출한 outer함수가 종료될 때까지 대기   
   7)outer함수 내부의 enviromentReacord 정보 수집   
   8)inner함수 선언문 수집   
   ------------------- outer함수 컨텍스트의 enviromentRecord 수집 끝   
   9)console.log(a); //---A 실행   
   변수 a를 outer context에서 탐색 → 변수 a없음 → 전역 context에서 탐색 → 1출력
   10)inner함수 정의는 앞에서 수집했으니깐 넘어가고 inner함수 호출   
   11)inner Excecution Context 활성화   
   12)var a 선언   
   ------------------- inner함수 컨텍스트의 enviromentRecord 수집 끝   
   13)console.log(a); //---B 실행   
   __변수 a가 inner Excecution Context에 선언은 돼있는데 값이 할당된 것이 아니기 때문에 undefined 발생__   
   14)변수 a에 3할당   
   15)inner함수에 대한 콜스택 반환, 스택에서 빠짐   
   ------------------- inner함수 context종료   
   16)console.log(a); //---C 실행   
   outer 컨텍스트에서 a탐색 → 없음 → 전역 context에서 탐색 → 1출력   
   17)outer context 종료   
   18)전역 컨텍스트에서 a탐색 → 1출력      
   19)프로그램 종료   
   20)전역 context 종료


1. #

   중첩 함수가 아니더라도 레시컬 환경이 적용될까요?
네, 중첩 함수가 아니더라도 일반 함수에도 레시컬 환경(Lexical Environment)이 적용됩니다.

레시컬 환경은 함수가 생성될 때 만들어지는 객체로, 함수가 참조할 수 있는 변수와 함수에 대한 정보를 담고 있습니다. 즉, 함수가 어디에서 선언되었는지에 따라 다른 레시컬 환경을 가지게 되고, 이를 통해 함수 내부에서 외부 변수에 접근하거나, 클로저를 생성하는 등의 동작이 가능해집니다.

왜 일반 함수에도 레시컬 환경이 필요할까요?
외부 변수 참조: 함수 내부에서 외부에서 선언된 변수를 참조할 수 있도록 합니다.
클로저 생성: 함수가 외부 변수를 기억하여 클로저를 생성할 수 있도록 합니다.
함수 스코프: 함수마다 독립적인 스코프를 제공하여 변수 충돌을 방지합니다.
예시:
JavaScript
let x = 10;

function outerFunction() {
  console.log(x); // 외부 변수 x에 접근

  function innerFunction() {
    console.log(x); // 외부 변수 x에 접근
  }

  innerFunction();
}

outerFunction(); // 10, 10 출력
코드를 사용할 때는 주의가 필요합니다.

위 예시에서 innerFunction은 outerFunction의 내부에서 선언되었지만, x 변수에 접근할 수 있습니다. 이는 innerFunction이 outerFunction의 레시컬 환경을 상속받기 때문입니다.

결론
레시컬 환경은 함수의 기본적인 동작 원리 중 하나이며, 중첩 함수뿐만 아니라 모든 함수에 적용됩니다. 레시컬 환경 덕분에 자바스크립트는 유연하고 강력한 함수형 프로그래밍 기능을 제공할 수 있습니다.

추가 설명
렉시컬 스코핑: 레시컬 환경은 코드가 작성된 순서(정적 스코핑)에 따라 결정됩니다. 런타임에 함수가 호출되는 위치에 따라 스코프가 결정되는 다이나믹 스코핑과는 다릅니다.
클로저: 함수와 그 함수가 생성된 렉시컬 환경의 조합을 클로저라고 합니다. 클로저는 함수형 프로그래밍에서 매우 중요한 개념이며, 데이터 은닉, 모듈화 등 다양한 용도로 활용됩니다.

