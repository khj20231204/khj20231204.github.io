---
layout: single
title: 5-1 옳바른 괄호
categories: CODINGTEST
tag: []
---

1. # 문제 설명
   괄호가 바르게 짝지어졌다는 것은 '(' 문자로 열렸으면 반드시 짝지어서 ')' 문자로 닫혀야 한다는 뜻입니다. 예를 들어.

   "()()" 또는 "(())()" 는 올바른 괄호입니다.
   ")()(" 또는 "(()(" 는 올바르지 않은 괄호입니다.
   '(' 또는 ')' 로만 이루어진 문자열 s가 주어졌을 때, 문자열 s가 올바른 괄호이면 true를 return 하고, 올바르지 않은 괄호이면 false를 return 하는 solution 함수를 완성해 주세요.

   제한사항
   문자열 s의 길이 : 100,000 이하의 자연수
   문자열 s는 '(' 또는 ')' 로만 이루어져 있습니다.

   입출력 예   

   |    s    | answer |
   |:-------:|:------:|
   |  "()()" |  true  |
   |"(())()" |  true  |
   |  ")()(" |  false |
   | "(()("  |  false |
   	
   입출력 예 설명
   입출력 예 #1,2,3,4
   문제의 예시와 같습니다.

1. # 풀이
   ※(())))(( 이거와 같은 경우 주의!   
   처음 ')' 인 경우 false   
   이후   
   if(c == '(') queue.offer(1);   
   if(c == ')') queue.poll();   
   이 조건만 따지게 되는 경우 (())))(( 이러한 경우 error발생   
   그렇기 때문에 중간에   
   if(queue.peek() == null) null인 경우 체크   

   '(' 와 ')'가 들어간 순서에 따라 앞에서부터 제거할 수 있고 뒤에서부터 제거할 수 있습니다. 앞에서부터 제거하기 위해선 queue를 사용해야 하고, 뒤에서 제거하기 위해선 stack을 사용해야 합니다. queue를 사용하고 stack을 사용한다는 조건 외엔 다른 점은 없습니다. 앞에부터 제거해도 갯수가 일치한 만큼 제거가 되고 부족하면 null이 발생할 것이며, 뒤에서부터 제거해도 갯수가 일치한 만큼 제거가 되고, 부족하면 null이 발생하기 때문입니다.   
   
   queue사용   
   ```java
      Queue<Integer> queue = new LinkedList<>();

      for(char c : s.toCharArray()){
         if(c == '(') queue.offer(1);
         if(queue.peek() == null) return false;
         if(c == ')') queue.poll();
      }

      return (queue.peek() == null) ? true : false;
   ```   
   queue는 인터페이스만 제공하기 때문에 상속받은 LinkedList를 이용해야 합니다.   
   
   stack사용   
   ```java
      Stack<Integer> stack = new Stack<>();

      for(char c : s.toCharArray()){
         
         if(c == '(') stack.push(1);
         if(stack.empty()) return false;
         if(c == ')') stack.pop();
      }

      return (stack.empty()) ? true : false;
   ```   
   Stack은 클래스로 제공이 되기 때문에 Stack자체를 이용할 수 있습니다.
   queue를 사용하든 stack을 사용하든 일반 조건은 같습니다. 그렇기 때문에 위에 queue를 stack으로 바꾼 것 외엔 변경사항이 없습니다.   
   현재 조건이 '(', ')', null 3가지기 때문에 else if를 사용하지 않았습니다. 조건을 다음과 같이 변경할 수 있습니다.   

   ```java
      if(c == '(') stack.push(1);
      else if(c == ')') {
         if(stack.empty()) return false;
         stack.pop();
      }
   ```   
   else if 조건으로 "c == ')'" 를 사용할 수 있습니다.   

1. # 풀이 2
   queue과 stack의 기능은 조건이 맞으면 엘리먼트 값을 넣고 삭제하고, 비었으면 null인지를 확인하는 기능밖에 없습니다. 특정한 값을 뽑는다던지, 특별히 입출력 순서를 고려할 필요도 없습니다. 단지 '(' 와 ')'의 순서에 따라 queue와 stack의 증가, 감소만 확인하면 됩니다. 특별한 순서의 고려가 없기 때문에 일반 변수로 나타낼 수도 있습니다.   

   ```java
      int count = 0;
      for(char c : s.toCharArray()){         
         if(c == '(') count++;
         if(count == 0) return false;
         if(c == ')') count--;
      }

      return (count == 0) ? true : false;
   ```   
   count란 변수를 설정 후 증감과 감소와 0으로 '(' 와 ')' 의 입출력을 체크합니다.   
   
