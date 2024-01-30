---
layout: single
title: 자바로 퀵 정렬
categories: CODINGTEST
tag: []
---

1. # 분석
   퀵 정렬이라하면 비교할 pivot을 선정 후 해당 배열의 인덱스 값에서 왼쪽으로 부터는 pivot보다 큰 값을 탐색, 오른쪽으로 부터는 pivot보다 작은 값을 탐색, 양쪽에 적절한 값이 탐색되면 서로 위치를 바꿔주고 왼쪽에서 증가값과 오른쪽에서 감소값이 교차가되면 오른쪽의 감소값이 새로운 배열의 끝나는 지점이 되고, 왼쪽의 증가값은 새로운 배열의 시작값이 되어 다시 나누어진 범위에서 탐색을 하는 재귀적 방법을 말합니다.   
   하지만 여기서는 인덱스로 탐색하는 과정없이 새로운 list를 2개 만들어 pivot과 값을 비교 후 작은 값들은 작은 값대로 새로운 list에 넣고, 큰 값들은 큰 값대로 새로운 list에 입력 후 "작은 값 + pivot + 큰 값"순으로 다시 list에 입력 후 하나의 범위로 합치게 되는 방법을 보입니다.

   ```java
      List<Integer> quickSort(List<Integer> list){
         //인덱스로 탐색하는 과정없이 바로 pivot과 값을 비교해서 덩어리로 나누고
         //나눈 덩어리를 다시 재귀로 원소 1개가 남을 때까지 계속 나눈다.

         if(list.size()<=1) return list; //원소가 1개가 남을 때까지 작은 부분과 큰 부분으로 계속 나눔

         int pivot = list.remove(0); //index 탐색과정이 없기 때문에 remove로 list의 모든 값들을 비교

         List<Integer> lesser = new ArrayList<>();
         List<Integer> greater = new ArrayList<>();

         for(int i=0; i<list.size() ; i++){
            if(pivot > list.get(i)) lesser.add(list.get(i)); //pivot과 값을 비교 후 작은 값을 list에 입력
            else greater.add(list.get(i)); //pivot과 값을 비교 후 큰 값을 list에 입력
         }

         List<Integer> merge = new ArrayList<>();
         merge.addAll(quickSort(lesser)); //quickSort에 넣는 건 나누어진 작은 쪽
         merge.add(pivot);
         merge.addAll(quickSort(greater)); //qucikSort에 넣는 건 나누어진 큰 쪽

         return merge;
      }
   ```   
   meger.addAll(quickSort(lesser));   
   meger.add(pivot);   
   meger.addAll(quickSort(greater));   
   이 부분에서 pivot보다 작은 부분은 재귀적으로 계속 나눠져 원소가 1개 남았을 때 lesser+pivot+greater 로 합쳐지면서 개별 원소들이 merge된 상태로 값을 계속 돌려주기 때문에 나중엔 하나의 집합이 되는 형태를 취하는데, 이건 "각각의 원소로 잘개 쪼갠 후 비교하면서 새로 병합을 하는" 병합정렬과 유사합니다. 반복문을 통해 비교하며 원소를 나누는 방식과 쪼갠 후 비교하며 병합하는 차이라 할 수 있습니다. 알고리즘이란 어떻게 생각하냐에 따라 무수한 방법이 있기 때문에 어렵습니다..


