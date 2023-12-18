---
layout: single
title: 2-1. 최댓값 인덱스 구하기
categories: CODINGTEST
tag: [array, list]
---

```java
   int max = 0, num = 0;
   for(int a : arr) if(a>max) {max = a; num++;}

   int count = 0;
   for(int a: arr) if(a == max) count++;

   int[] answer = new int[count];
   int index = 0;
   for(int i=0  ;i<arr.length; i++){
      if(arr[i] == max) answer[index++] = i;
   }

```

```java
   public int[] solution(int[] arr) {
       
        //최댓값 구하기
        int max = 0;
        for(int a : arr) if(a>max) {max = a;}
        
        //리스트 생성
        List<Integer> list = new LinkedList<>();
        for(int i=0 ; i<arr.length ; i++){
            if(arr[i] == max) list.add(i);
        }
        
        //리스트를 배열로
        int[] answer = new int[list.size()];
        int num = 0;
        for(int i=0 ; i<list.size() ; i++){
                answer[num++] = list.get(i);
        }
        
        return answer;
    }
```