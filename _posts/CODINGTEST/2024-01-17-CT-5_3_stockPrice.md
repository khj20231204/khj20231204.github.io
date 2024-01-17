---
layout: single
title: 5-3 주식 가격
categories: CODINGTEST
tag: []
---

1. # 문제 설명
   초 단위로 기록된 주식가격이 담긴 배열 prices가 매개변수로 주어질 때, 가격이 떨어지지 않은 기간은 몇 초인지를 return 하도록 solution 함수를 완성하세요.

   제한사항
   prices의 각 가격은 1 이상 10,000 이하인 자연수입니다.
   prices의 길이는 2 이상 100,000 이하입니다.
   
   입출력 예

   |     prices    |     return    |
   |:-------------:|:-------------:|
   |[1, 2, 3, 2, 3]|[4, 3, 1, 1, 0]|
   	
   입출력 예 설명
   1초 시점의 ₩1은 끝까지 가격이 떨어지지 않았습니다.
   2초 시점의 ₩2은 끝까지 가격이 떨어지지 않았습니다.
   3초 시점의 ₩3은 1초뒤에 가격이 떨어집니다. 따라서 1초간 가격이 떨어지지 않은 것으로 봅니다.
   4초 시점의 ₩2은 1초간 가격이 떨어지지 않았습니다.
   5초 시점의 ₩3은 0초간 가격이 떨어지지 않았습니다.
   
1. # 풀이
   ```java
      public int[] solution(int[] prices) {
        int[] answer = {};
        
        //List<Integer> pricesList = Arrays.stream(prices).boxed().collect(Collectors.toList());
        Queue<Integer> queue = new LinkedList<>();
        Stack<Integer> stack = new Stack<>();
        //자신보다 크거나 같으면 count++, 자신보다 작으면 count입력
        
        for(int i=0 ; i<prices.length-1 ; i++){ //제일 마지막 값은 무조건 0 이기때문에 비교할 필요가 없음
            int a = prices[i];
            int count = 0; //핵심! count를 언제 증가 시키나. 자기보다 작은 놈이 나와도 1증가, 자기보다 큰 놈이 나와도 1증가
            boolean check = true;
            for(int j=i+1 ; j<prices.length ; j++){
                int b = prices[j];
                if(a<=b){ //자신보다 크거나 같으면 count++
                    
                    count++;
                    System.out.println("count:"+count);
                }else{ //자신보다 작으면 count입력
                    stack.push(count);
                    count = 1;
                    check = false;
                    break;
                }
            }
            
            //핵심! 가격이 떨어져서 break를 해도 이쪽으로 나오고, 끝까지 더 증가 해서 안쪽 for문이 끝나도 이쪽으로 나온다
            if(check) stack.push(count);
        }
       
        stack.push(0);
        System.out.println(stack);
        
        return answer;
    }
   ```