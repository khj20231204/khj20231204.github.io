---
layout: single
title: 재귀함수 - 유클리드 호제법
categories: CODINGTEST
tag: []
---

1. # 분석
  30 96과 같은 이런 간단한 수는 소인수분해로 최대공약수를 구할 수도 있지만, 13632, 33445와 같이 큰 수는 조립제법으로 구하기 까다롭습니다. 이럴 때 유클리드 호제법을 개선한 방법을 이용해서 최대공약수를 구하면 편합니다.  

   유클리드 호제법 개선   
   1.큰 수를 작은 수로 나뉜다.   
   2.나눈 나머지로 다시 작은 수를 나눕니다.   
   3.나머지가 0이 될 때까지 반복합니다.

  30과 96을 예로 들겠습니다.   
  96 % 30 = 6(몫이 아니라 나머지가 6)   
  30 % 6 = 6   
  작은 수와 나머지가 일치 ⇒ 최대 공약수는 6   

  코드는 다음과 같습니다.   
  ```JAVA
   public static void main(String[] args){
      EuclideanRecursive.euclideanRecursive(30,96);
   }

   int euclideanRecursive(int shortSide, int modNumber){

      if(modNumber == 0) return shortSide;

      return shortSide > modNumber ? euclideanRecursive(modNumber, shortSide%modNumber) : euclideanRecursive(shortSide, modNumber%shortSide);
      }                                           
  ```   
  return에의해 함수를 호출한 쪽으로 돌아갈 때 특별한 연산을 하지 않았기 때문에 재귀에서 최종적으로 나머지가 0일 때 리턴된 shortSide변수를 그대로 쭉 가지고 갑니다.   
  
  euclideanRecursive(30, 96)이나 euclideanRecursive(96, 30)처럼 매개변수로 큰 숫자가 앞에 올지 뒤에 올지 모르기 때문에 return 문을 조건식으로 구현했습니다. 


