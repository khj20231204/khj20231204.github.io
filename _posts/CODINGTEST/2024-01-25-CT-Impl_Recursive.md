---
layout: single
title: 재귀함수
categories: CODINGTEST
tag: []
---

1. # 재귀함수 특징
   ```java
      public static void main(String[] args){
         Recursive.recursive(5);
      }

      void recursive(int num){

         if(num <= 0) return;

         System.out.println(num + " before recursive"); //재귀 실행 전 --- ㉠ 
         recursive(num-1);
         System.out.println(num + " after recursive"); //재귀 실행 후 --- ㉡
      }

      결과 : 
      5 before recursive
      4 before recursive
      3 before recursive
      2 before recursive
      1 before recursive
      1 after recursive
      2 after recursive
      3 after recursive
      4 after recursive
      5 after recursive
   ```   
   함수는 __호출__ 될 때 마다 __메모리상에 공간을 차지__ 합니다.   
   함수가 __종료__ 되거나 __리턴__ 이 되면 __호출한 쪽으로 돌아가며 메모리에서 삭제__ 됩니다.   
   재귀 함수는 재귀를 호출 전(㉠)과 호출 후(㉡) 실행 시기에서 차이가 있습니다. ㉡은 재귀 함수 호출 후 실행이 되기 때문에 가장 먼저 실행이 되었던 num=5는 메모리를 차지만 하고 대기하고 있는 상태가 됩니다. 가장 마지막 재귀함수가 종료가 되어서야 실행되기 때문에 num=1부터 실행이 됩니다. recuersive의 매개변수 num이 조건을 만족하여 return을 할 때까지 모든 밑 부분(여기서는 ㉡)의 실행은 정지되어 대기 상태가 됩니다.   
   반면 ㉠은 재귀함수와는 큰 관련이 없기 때문에 단순 호출이 발생할 때마다 출력 되므로 num 값이 5,4,,..1 순서로 출력됩니다.   
   재귀적 방식은 대부분 반복문으로 수행이 가능하기 때문에 가능하면 반복문을 사용하는 것이 메모리 관리, 실행속도, 가독성면에서 효율적입니다.   
   


