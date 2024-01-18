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
                    count++; //자신보다 큰 경우라는 조건에서 count++를 하게 되는데 이 조건이 밖에 나갈 수도 있다
                }else{ //자신보다 작으면 count입력
                    stack.push(count);
                    check = false;
                    break;
                }
            }
            //핵심! 가격이 떨어져서 break를 해도 이쪽으로 나오고, 끝까지 더 증가 해서 안쪽 for문이 끝나도 이쪽으로 나온다
            if(check) stack.push(count);
        }       
        stack.push(0);
        
        return answer;
    }
    ```   
    이 문제 핵심은 [1,2,3,2,3]에서 1→2 1이 2가 될 때도 1이 증가, 3→2 3이 2가 될 때도 1이 증가한다는 조건입니다. "값이 커져도 증가, 값이 작아져도 증가"하는 부분인데 이걸 코딩하면   
    ```java
    for(int i=0 ; i<prices.length-1 ; i++){ 
            int count = 0; // ☜ ㉠
            ...
            for(int j=i+1 ; j<prices.length ; j++){
                int b = prices[j];
                if(a<=b){ 
                    count++;
                }else{ 
                    stack.push(count);
                    ...
                    break;
                }
            }
        ... 
    ```   
    ㉠ 이 부분을 count=0으로 하면 [1,2,3,2,3]에서 1,2,2 인 부분에서 1씩 부족한 결과가 나오게 되고,
    count=1로 하게되면 3→2인 부분에서 1이 더 증가한 결과가 발생하게 됩니다.   
    문제 조건을 보면 "앞에 수보다 뒤에 수가 더 크면 증가를 하게 된다"란 조건이 나오게 됩니다. 1을 예로 들면 1 → 2 일 때 1증가, 1 → 3 또 1증가, 1 → 2 또 1증가, 1 → 3 또 1증가. 그렇기 때문에 조건식 안에서 count를 증가시키 코드를 작성하게 됩니다.   
    ```java
    for(int i=0 ; i<prices.length-1 ; i++){ 
        ...
        for(int j=i+1 ; j<prices.length ; j++){
            if(a<=b){  // ← b가 더 큰 경우에
                count++;  //count증가
            }else{ ... }
        ... 
    ```   
    하지만 이렇게 a<=b란 조건과 a>b란 조건으로 나뉘게 되면 올바른 결과를 얻을 수 없습니다.   
    조건을 나눠서 증가를 시킨다는 생각을 바꿔야 합니다. 값이 작아져도 1이 증가, 값이 커져도 1이 증가 한다는 말을 다른 뜻으로 생각해보면 "값이 1 증가하고 시작한다"가 됩니다. 이것은 최초 count를 1로 선언하는 것과 다른 의미가 됩니다.    
    ```java
        for(int i=0 ; i<prices.length-1 ; i++){ 
        ...

        for(int j=i+1 ; j<prices.leng   th ; j++){
            count++;  //count증가
            if(a<=b){  // ← b가 더 큰
            }else{ 
        ... 
    ```   
    if문 앞에서 count를 증가 시키고, if(a<=b)일 때 count++를 증가시키지 않기 때문에 원하는 값을 얻을 수가 있습니다.   

    수정된 전체 소스 입니다.   
    ```java
        public int[] solution(int[] prices) {
        int[] answer = {};
        
        Stack<Integer> stack = new Stack<>();
        
        for(int i=0 ; i<prices.length ; i++){ 
            int a = prices[i];
            int count = 0; //<- 0을 해야 가장 마지막 요소값에 0 입력 됨
            for(int j=i+1 ; j<prices.length ; j++){
                int b = prices[j];
                count++;
                if(a>b) break;
            }
            stack.push(count);
        }
       return stack.stream().mapToInt(Integer::intValue).toArray();
    }
    ```
