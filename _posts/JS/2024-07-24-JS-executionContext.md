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

   실행 컨텍스트에는 세 가지 환경 정보가 있습니다.   
   VariableEnviroment : 식별자 정보 수집    
   LexicalEnviroment : 각 식별자의 '데이터' 추적   
   ThisBinding   
    
   VariableEnviroment는 오직 식별자 정보를 수집하는 용도로 사용됩니다. 컨텍스트 내부 코드들을 실행 하는 동안에 변화되는 값들은 LexicalEnviroment에 실시간으로 반영이 됩니다.   
   VariableEnviroment는 실시간 변화 반영X   
   LexicalEnviroment는 실시간 변화 반영O  
   VariableEnviroment와 LexicalEnviroment의 차이는 실시간 반영 여부만 있습니다.   

   LexicalEnviroment는 어휘적 환경, 사전적인 환경이라고 합니다.   
   
   |    영한 사전     |         실행 컨텍스트A 환경 사전      |
   |:---------------:|:------------------------------------:|
   |  able:할 수 있는 | 내부식별자a : 현재 값은 undefined이다 |
   |  apple:  사과   |      내부식별자b : 현재 값은 20이다    |
   |arrow:화살, 화살표|         외부 정보 : D를 참조한다      | 

   LexicalEnviroment   
   1)enviromentRecord : 현재 문맥의 식별자 정보 저장   
   2)outerEnviromentReference : 외부 문맥의 식별자 정보 저장    

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
   함수정의 선언된 1)만 함수 전체가 끌어올려지고 2),3) 함수 표현식으로 작성된 경우 할당된 참조변수만 끌어올려집니다.   



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
         console.log(a);

         function inner(){    //inner함수 정의
            console.log(a);
            var a = 3;
         }

         inner();             //inner함수 호출
         console.log(a);
      }

      outer();                //outer함수 호출
   ```   
   1)전역 Excecution Context활성화    
   2)변수 a 선언(할당은 아님 a는 undefined)   
   3)함수 outer 선언   
   ------------------- 전역 컨텍스트의 enviromentRecord 수집 끝   
   4)변수 a에 1할당   
   5)함수 outer 호출 → OUTER Excecution Context 활성화   
   6)"outer함수 호출"은 호출한 outer함수가 종료될 때까지 대기   
   7)outer함수 내부의 enviromentReacord 정보 수집   
   8)inner함수 선언문 수집   
   ------------------- inner함수 컨텍스트의 enviromentRecord 수집 끝   
   9)console.log(a);

