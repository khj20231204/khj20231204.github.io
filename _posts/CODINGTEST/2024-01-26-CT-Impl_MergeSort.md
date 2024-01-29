---
layout: single
title: 병합 정렬
categories: CODINGTEST
tag: []
---

1. # 분석   
   "각각의 원소들로 먼저 쪼갠 후 → 값을 비교하며 병합하는 정렬"   
   주어진 배열들을 각각의 원소들이 1개가 될 때까지 먼저 인덱스를 이용해서 나눕니다.   
   가장 왼쪽 인덱스, 가장 오른쪽 인덱스를 반으로 나눈 중간 인덱스 mid를 구합니다. 그렇게 되면 범위는 왼쪽부터 mid까지, mid+1부터 오른쪽 인덱스까지 2개의 범위로 나눠집니다.   
   나누어진 한 범위의 mid 값을 구해서 다시 2개의 범위를 나누고,... 이와 같은 작업을 1개의 원소로 나눠질 때까지 실행합니다.   
   Merge병합은 첫번째는 나누는 것입니다. 각각 1개의 원소로 index로 나눠서 이후, 새로운 배열을 이용해서 값을 집어 넣을 때 그때 비교를 하면서 병합을 수행하게 됩니다.   

   int mid = (left+right)/2; 
   mid값을 구합니다.   

   mergeSortUtility(array, arrayCopy, left, mid);   
   left부터 mid까지 하나의 범위가 되고

   mergeSortUtility(array, arrayCopy, mid+1, right);   
   mid+1부터 right까지 하나의 범위가 됩니다.   

   이런 식으로 재귀호출을 하다보면 left와 right가 같아질 때가 있는데 그 때가 1개의 원소로 전부 나눠졌을 때가 됩니다.

   [3,4,5,1,8,4,9] 9개의 배열이 있을 때 재귀적으로 나눠지는 순서만 보면 다음과 같습니다.      
   *[] 안에 값은 index값입니다.   
   left 1번 재귀 : left[0] - mid[2] - right[5]   
   left 2번 재귀 : left[0] - mid[1] - right[2]   
   left 3번 재귀 : left[0] - mid[0] - right[1]   
   left 4번 재귀 : left[0] - mid[0] - right[0]   
   left == right이므로 종료   
   왼쪽 1개의 원소로 나눔   

   left 3번 재귀 : left[0] - mid[0] - right[1]를 가지고 왼쪽부분은 다 나눴으니 오른쪽 부분을 재귀적으로 나눕니다.   
   right 1번 재귀 : left[1] - mid[1] - right[1]   
   left == right이므로 종료   
   *left와 right가 같은 left[1] - mid[1] - right[1] 재귀는 메모리에서 사라지고,   
   left 3번 재귀 left[0] - mid[0] - right[1]에서 sorting을 하게 됩니다.   

   sorting: left[0] - mid[0] - right[1]   
   -------- 첫 번째와 두 번째 원소 병합 정렬 끝 --------   

   *3번 재귀가 끝났기 때문에 2번 재귀부터 시작   
   left 2번 재귀 : left[0] - mid[1] - right[2]   
   right 1번 재귀 : left[2] - mid[2] - right[2]   
   left == rgith이므로 종료   

   sorting : left[0] - mid[1] - right[2]   
   -------- 첫 번째부터 세 번째 원소까지 병합 정렬 끝 --------   

   1번 재귀 : left[0] - mid[2] - right[5]   
   right 1번 재귀 : left[3] - mid[4] - right[5]   
   right 2번 재귀 : left[5] - mid[5] - right[5]   
   left == right 이므로 종료   

   sorting : right 1번 재귀 left[3] - mid[4] - right[5]   
   -------- 네 번재 원소부터 마지막 원소까지 오른쪽 병합 정렬 끝 --------   

   1번 재귀 : left[0] - mid[2] - right[5]   
   
   sorting : left[0] - mid[2] - right[5]   
   -------- 첫 번재 원소부터 마지막 원소까지 병합 정렬 끝 --------   


   ```java
      void mergeSort(int[] array){
         int[] arrayCopy = new int[array.length];

         mergeSortUtility(array, arrayCopy, 0, array.length-1);
      }
   ```   
   arrayCopy라는 임시 저장 배열을 생성해야하기 때문에 mergeSortUtility란 새로운 메소드에서 병합정렬을 구현합니다.   
   정렬 시에 array에 값을 arrayCopy로 복사해서 arrayCopy값을 비교 후 array에 다시 병합 정렬하게 됩니다.   
   
   ```java
      void mergeSortUtility(int[] array, int[] arrayCopy, int left, int right){
        int mid = (left+right)/2;
        System.out.println("left:"+left+" ,right:"+right);
        if(left < right) { //left == right 경우 재귀를 멈추고 다음 코드 진행
            mergeSortUtility(array, arrayCopy, left, mid); //왼쪽 원소가 1개 남을 때까지 나눈다
            mergeSortUtility(array, arrayCopy, mid + 1, right); //오른쪽 원소가 1개 남을 때까지 나눈다
            sorting(array, arrayCopy, left, mid, right); //left, mid, right의 인덱스로 배열을 나눔
        }
    }
   ```   
   mergeSortUtility(array, arrayCopy, left, mid);로 왼쪽부터 전부 나눈 후   
   mergeSortUtility(array, arrayCopy, mid + 1, right);로 오른쪽을 나누고,   
   left == right가 되었을 때 재귀를 종료하고 
   right 1번 재귀 : left[1] - mid[1] - right[1]  에서 종료 후 → left 3번 재귀 left[0] - mid[0] - right[1]에서 병합 정렬을 한 것과 같이 바로 __이전에 상태로 돌아가서__ 정렬을 수행하게 됩니다.    

   ```java
      static void sorting(int[] array, int[] arrayCopy, int left, int mid, int right){
         System.out.println("left:"+left+" ,right:"+right);

         int idxMerge = left; //임시 저장 배열 index역시 left부터

         //나뉘는 범위 left1~mid / mid+1(left2)~right
         //index로 배열을 나눠서 2개의 배열로 보고 병합을 한다
         int idxLeft1 = left;
         int idxLeft2 = mid+1;

         /*
         메소드끼리 주고 받는 배열은 array이기 때문에 array를 이동 시켜서 결과값을 가져오기 위해 현
         재 array에 있는 값을 arrayCopy에 복사를 해서 arrayCopy에서 비교 후 array에 집어넣는다.
         */
         for(int i=left ; i<=right ; i++) arrayCopy[i] = array[i];

         while(idxLeft1<=mid && idxLeft2<=right){ //idxLeft1~mid | idxLeft2(mid+1)~right을 2개의 배열로 보고 값을 비교
            if(arrayCopy[idxLeft1] < arrayCopy[idxLeft2]){
                  array[idxMerge++] = arrayCopy[idxLeft1++];
            }else{
                  array[idxMerge++] = arrayCopy[idxLeft2++];
            }
         }

         while(idxLeft1<=mid) array[idxMerge++] = arrayCopy[idxLeft1++]; 
         //idxLeft2(오른쪽 배열)가 먼저 정렬이 끝난 경우 idxLeft1의 나머지 배열 값들을 전부 입력
         while(idxLeft2<=right) array[idxMerge++] = arrayCopy[idxLeft2++];
         //idxLeft1(왼쪽 배열)이 먼저 정렬이 끝난 경우 idxLeft2의 나머지 배열 값들을 전부 입력
      }
   ```   
   실제 병합정렬을 하는 코드입니다. 값을 비교하기 위해 arrayCopy라는 배열에 array값을 __left부터__ 복사를 합니다. arrayCopy에 있는 값들이 left부터 mid까지가 하나의 배열 범위가 되고, mid+1부터 right까지가 하나의 배열이 되어 두 배열의 값을 비교 후 array배열에 입력합니다. 병합 정렬이 이루어지는 이 코드 부분은 앞서 배열의 모든 원소들을 1개씩 전부 나누고 난 이후에 비소로 순차적으로 병합하며 실행되게 됩니다.
   
