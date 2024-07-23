---
layout: single
title: 퀵 정렬
categories: CODINGTEST
tag: []
---

1. # 분석
   퀵 정렬은 비교 대상을 정한 후 왼쪽에서의 값과 오른쪽에서의 값을 비교 후 왼쪽 값이 비교 대상 값보다 더 크거나 같은 경우, 오른쪽 값이 비교 대상 값보다 더 작거나 같은 경우 왼쪽과 오른쪽 서로를 교환하는 방식으로 정렬해 나가게됩니다. 여기서 비교 대상이 되는 값을 pivot이라 하며, pivot은 단지 비교 대상의 값일 뿐 배열된 원소들의 왼쪽 인덱스와 오른쪽 인덱스의 증가와 감소엔 아무런 관여를 하지 않습니다.   

   *pL, pR은 index   
   
   pL은 가장 왼쪽의 인덱스 값   
   pR은 가장 오른쪽의 인덱스 값   

   pivot = (pL+pR)/2 로 중간 index값으로 선택   

   3 6 1 9 7 4 : pivot을 index=2인 1로 선택, pL=0, pR=5, arr[L]=3, arr[R]=4   
   
   pL은 → 방향으로 증가하면서 pivot값 1보다 크거나 같은 수를 검색   
   pR은 ← 방향으로 감소하면서 pivot값 1보다 작거나 같은 수를 검색   

   __3(pL)__ 6 __1(pR)__ 9 7 4 : pL=0, pR=2, arr[0]=3, arr[2]=1(pviot과 같음) → 스왑   

   *스왑은 숫자만 해당, index는 상관 없음   
   스왑 이후 L은 계속 증가, R는 계속 감소   

   __1(pL)__ 6 __3(pR)__ 9 7 4   

   __1(pR)__ __6(pL)__ 3 9 7 4 : pL과 pR이 교차되었습니다. 범위를 새로 나눕니다.   

   __1(pR)__ 6 3 9 7 4 : pL은 계속 증가하여 pL>Right 가 되어 종료, pR=0, arr[0]=1에서 검색 종료   

   left = 0;   
   pR = 0;   
   right = 5;   
   pL = 1;   

   if(left < pR) quickSort(arr, left, pR); 해당 없음   
   if(pL < right) quickSort(arr, pL, right);   

   1 __6(pL)__ 3 9 7 __4(pR)__   

   mid값은 (1+5)/2 = 3, index=3의 pivot = 9   

   → 방향 : 9보다 크거나 같은 수 선택   
   ← 방향 : 9보다 작거나 같은 수 선택   

   1 6 3 __9(pL)__ 7 __4(pR)__  : 9와 4를 스왑   

   1 6 3 __4(pL)__ 7 __9(pR)__ : pL은 계속 증가, pR은 계속 감소   

   1 6 __3(pR)__ 4 7 __9(pL)__ : pR과 pL이 교차 되었음,

   left = 1;
   pR = 2;
   right = 5;
   pL = 5;

   if(left < pR) quickSort(arr, left, pR); 다시 재귀 호출   
   if(pL < right) quickSort(arr, pL, right); 해당 없음   

   ...

   이런 식으로 계속 재귀 호출을 하여 pL과 pR의 값으로 탐색을 하는 방식입니다.   

   ```java
      void quickSort(int[] arr, int left, int right){
         int pL = left;
         int pR = right;
         int pivot = arr[(pL+pR)/2]; //pivot구하기

         while(pL < pR) {

            while (arr[pL] < pivot) pL++;
            while (arr[pR] > pivot) pR--;

            int tmp = arr[pL];
            arr[pL] = arr[pR];
            arr[pR] = tmp;
            pL++; //값 교체 후 pL증가 
            pR--; //값 교체 후 pR감소

         }

         if(left < pR) quickSort(arr, left, pR);
         if(pL < right) quickSort(arr, pL, right);
      }
   ```   
   pivot을 구한 후 pivot보다 작거나 같은 경우 혹은 크거나 같은 경우를 검색하여 __스왑을 한 후 pL은 증가 시키고, pR은 감소__ 를 시킵니다. 만약 스왑을 한 후 다음과 같은 증감이 없으면 무한루프에 빠지게 됩니다. 이후 pL < pR 의 조건을 확인 후 pL과 pR의 순서가 교차가 되면 while문을 빠져나와 quickSort 재귀를 하게 됩니다.   
   if(left < pR)과 if(pL < right) 두개의 조건은 pR이 계속 감소하여 음수가 되는 경우, pL이 계속 증가하여 배열의 index범위를 넘어서는 것을 막아 줍니다.   


