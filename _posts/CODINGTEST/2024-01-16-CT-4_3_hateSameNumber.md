---
layout: single
title: 4-3 같은 숫자는 싫어
categories: CODINGTEST
tag: []
---

1. # 문제 설명
   배열 arr가 주어집니다. 배열 arr의 각 원소는 숫자 0부터 9까지로 이루어져 있습니다. 이때, 배열 arr에서 연속적으로 나타나는 숫자는 하나만 남기고 전부 제거하려고 합니다. 단, 제거된 후 남은 수들을 반환할 때는 배열 arr의 원소들의 순서를 유지해야 합니다. 예를 들면,

   arr = [1, 1, 3, 3, 0, 1, 1] 이면 [1, 3, 0, 1] 을 return 합니다.
   arr = [4, 4, 4, 3, 3] 이면 [4, 3] 을 return 합니다.
   배열 arr에서 연속적으로 나타나는 숫자는 제거하고 남은 수들을 return 하는 solution 함수를 완성해 주세요.

   제한사항
   배열 arr의 크기 : 1,000,000 이하의 자연수
   배열 arr의 원소의 크기 : 0보다 크거나 같고 9보다 작거나 같은 정수
   입출력 예

   |      arr      |  answer  |
   |:-------------:|:--------:|
   |[1,1,3,3,0,1,1]|[1,3,0,1] |
   | [4,4,4,3,3]   |   [4,3]  |	
   	
1. # 풀이
   간단한 문제입니다. 출력시 순서가 일정해야 하기 때문에 List를 사용하고, List에 add 하기 전 앞 숫자와 일치하는지 확인 후 다른면 add를 하지 않습니다.   

   ```java
      public int[] solution(int []arr) {
      
         ArrayList<Integer> list = new ArrayList<>();
         list.add(arr[0]);
         for(int i=1 ; i<arr.length ; i++){
            if(arr[i-1] != arr[i])
                  list.add(arr[i]);
         }

         return list.stream().mapToInt(Integer::intValue).toArray();`
    }
   ```   
   첫번째 배열 값을 입력시 반복문 전에 list.add(arr[0]);을 해주었는데 '-1'이란 임의의 값을 입력 후 확인 할 수도 있습니다.   

   ```java
      ArrayList<Integer> list = new ArrayList<>();
      int temp = -1; //-1이란 주어진 값보다 더 작은 값을 임의의 입력
      for(int i=0 ; i<arr.length ; i++){
         if(temp == arr[i]) continue;  //같으면 continue
         temp = arr[i];
         list.add(arr[i]);
      }
   ```   
   temp = -1; 이란 가장 작은 값을 대입하므로 첫번째 arr[0] 값은 항상 list에 add가 됩니다.   
   같으면 continue를 하게 되는데 for문의 바로 다음 i번째로 순서가 넘어갑니다.   
