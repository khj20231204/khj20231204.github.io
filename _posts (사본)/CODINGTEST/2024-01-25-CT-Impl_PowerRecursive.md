---
layout: single
title: 재귀함수 - 거듭제곱근 구하기
categories: CODINGTEST
tag: []
---

1. # 분석
   2＾0 = 1   
   2＾1 = 2   
   2＾2 = 4   
   2＾3 = 8   
   2＾4 = 16   
   ...

   xⁿ = y   
   n : 지수, X : 밑   
   x는 y의 n제곱근.   
   y는 x의 n제곱.   

   구해야하는 수는 y.   

   2＾4 = 2x(2＾3) = 2x(2x(2＾2)) = 2x(2x(2x(2＾1))) = 2x(2x(2x(2x(2＾0)))) = 16   

   지수 = 밑x(지수-1) 로 나타낼 수 있습니다. 밑x(지수-1)에서 지수는 다시 밑x(지수-1)로.. 이런 식으로 다시 자신을 불러옵니다.   
   
   밑 값과 지수값이 주어지면 지수 n이 1씩 감소하여 0이 될 때까지 재귀 호출을 하여 거듭제곱을 구할 수 있습니다.      

   ```java
      public static void main(String[] args){
         powerRecursive(2, 4);
      }
      
      int powerRecursive(int x, int n){
         if(n <= 0) return 1;

         return x * powerRecursive(x, n-1);
      }
   ```   
   지수 n을 0이 될 때까지 n-1로 계속 감소시킵니다. n=0이 되면 n=1을 리턴하고 대기하고 있던 x*(x*..(x*(x,n-1))) = x*x*x*x*..x 가 실행됩니다.   