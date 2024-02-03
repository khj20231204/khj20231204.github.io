---
layout: single
title: 7-1 제일 작은 수 제거하기
categories: CODINGTEST
tag: []
---

1. # 문제 설명
   정수를 저장한 배열, arr 에서 가장 작은 수를 제거한 배열을 리턴하는 함수, solution을 완성해주세요. 단, 리턴하려는 배열이 빈 배열인 경우엔 배열에 -1을 채워 리턴하세요. 예를들어 arr이 [4,3,2,1]인 경우는 [4,3,2]를 리턴 하고, [10]면 [-1]을 리턴 합니다.

   제한 조건   
   arr은 길이 1 이상인 배열입니다.   
   인덱스 i, j에 대해 i ≠ j이면 arr[i] ≠ arr[j] 입니다.   

   입출력 예

   |    arr  |  return |
   |:-------:|:-------:|
   |[4,3,2,1]| [4,3,2] |
   |   [10]  |   [-1]  |

1. # 풀이 1
   
   배열을 바로 리턴 : new int[] {-1};

   ```java
      public static int[] solution(int[] arr) {
        int len = arr.length;

        if (len <= 1) return new int[]{-1};

        int min = Arrays.stream(arr).min().getAsInt();
        int[] answer = new int[arr.length - 1];
        int cnt = 0;
        for (int i : arr) {
            if (i == min) continue;

            answer[cnt++] = i;
        }

        return answer;
    }
   ```   
   주의 할 점은 arr이 빈 배열일 수 있기때문에   
   if(len <= 1)   
   이 조건을 검색하기 전에   
   int[] answer = new int[arr.length - 1];   
   arr.length를 사용하면 안된다는 점.

1. # 풀이 2
   
   stream의 filter이용   

   ```java
      public static int[] solution2(int[] arr) {
        if (arr.length <= 1) return new int[]{-1};
        
        int min = Arrays.stream(arr).min().getAsInt();
        return Arrays.stream(arr).filter(a -> a != min).toArray();
      }
   ```
	