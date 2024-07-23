---
layout: single
title: 재귀함수 - 피보나치 수열
categories: CODINGTEST
tag: []
---

1. # 분석
   피보나치수열은 앞에 두 항의 합으로 뒤에 항을 결정하는 수열입니다. 가장 앞에 2개 항은 1이 됩니다.   
   
   1 1 2 3 5 8 13 21 ...

   앞에 2항을 재귀적 용법으로 계속 더하게 됩니다.   

   f(1) = f(2) = 1   
   f(n) = f(n-1) + f(n-2)  

   ```java 
      public static void main(String[] args){
         FibonacciRecursive.fibonacciRecursive(7);
      }

      int fibonacciRecursive(int n){

         if(n==1 || n==2) return 1;

         return fibonacciRecursive(n-1) + fibonacciRecursive(n-2);
      }
   ```   
   n이 1과 2일 때 1을 대입하고,   
   3이상인 경우 재귀적 호출을 합니다. return항에 f(n-1) + f(n-2)를 입력합니다.   
   
   f(6) = f(5) + f(4)   
   f(5) = f(4) + f(3)   
   ...
   f(3) = 1 + 1

   결국 f(6)과 f(5)는 __1을 계속 더해서 이루어진 결과값__ 이 됩니다.

