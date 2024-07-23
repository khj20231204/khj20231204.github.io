---
layout: single
title: 6-3 스킬트리
categories: CODINGTEST
tag: []
---

1. # 문제 설명
   선행 스킬이란 어떤 스킬을 배우기 전에 먼저 배워야 하는 스킬을 뜻합니다.

   예를 들어 선행 스킬 순서가 스파크 → 라이트닝 볼트 → 썬더일때, 썬더를 배우려면 먼저 라이트닝 볼트를 배워야 하고, 라이트닝 볼트를 배우려면 먼저 스파크를 배워야 합니다.

   위 순서에 없는 다른 스킬(힐링 등)은 순서에 상관없이 배울 수 있습니다. 따라서 스파크 → 힐링 → 라이트닝 볼트 → 썬더와 같은 스킬트리는 가능하지만, 썬더 → 스파크나 라이트닝 볼트 → 스파크 → 힐링 → 썬더와 같은 스킬트리는 불가능합니다.

   선행 스킬 순서 skill과 유저들이 만든 스킬트리1를 담은 배열 skill_trees가 매개변수로 주어질 때, 가능한 스킬트리 개수를 return 하는 solution 함수를 작성해주세요.

   -제한 조건-   
   - 스킬은 알파벳 대문자로 표기하며, 모든 문자열은 알파벳 대문자로만 이루어져 있습니다.   
   - 스킬 순서와 스킬트리는 문자열로 표기합니다.   
    예를 들어, C → B → D 라면 "CBD"로 표기합니다.   
   - 선행 스킬 순서 skill의 길이는 1 이상 26 이하이며, 스킬은 중복해 주어지지 않습니다.   
   - skill_trees는 길이 1 이상 20 이하인 배열입니다.   
   - skill_trees의 원소는 스킬을 나타내는 문자열입니다.   
    skill_trees의 원소는 길이가 2 이상 26 이하인 문자열이며, 스킬이 중복해 주어지지 않습니다.   

   입출력 예

   | skill |             skill_trees           | return |
   |:-----:|:---------------------------------:|:------:|
   | "CBD" | ["BACDE", "CBADF", "AECB", "BDA"] |    2   |


   입출력 예 설명
   - "BACDE": B 스킬을 배우기 전에 C 스킬을 먼저 배워야 합니다. 불가능한 스킬트립니다.   
   - "CBADF": 가능한 스킬트리입니다.   
   - "AECB": 가능한 스킬트리입니다.   
   - "BDA": B 스킬을 배우기 전에 C 스킬을 먼저 배워야 합니다. 불가능한 스킬트리입니다.   

1. # 풀이 1
   skill_trees에서 skill만 남기도 모두 제거 후 skill_trees가 skill로 시작하는지 찾는 것과 같은 문제입니다.   
   skill_trees에서 skill 이외 문자를 모두 지웁니다.   
   BACDE → BCD   
   CBADF → CBD   
   AECB → CB   
   BDA → BD   
   
   CBD를 BCD, CBD, CB, BD로 시작하는지 확인하면 됩니다.   

   이때 String클래스의 startsWith와 replaceAll이 사용됩니다.   

   startsWith는 주어진 문자열로 시작하는지 확인 하는 메소드입니다.   

   replace와 replaceAll가 있는데, 이 두 개의 차이점은 replace는 변환할 문자를 넣게되는데 replaceAll은 정규표현식을 사용할 수 있습니다.   
   ```java
      String s1 = "abcd";
      s1.replace("[ab]",""); //abcd
      s1.replaceAll("[ab]",""); //cd
   ```   
   replace는 문자나 문자열만 가능하지만 replaceAll은 "[ab]"와 같은 정규표현식이 가능합니다.   

1. # 풀이 1
   ```java
      for(String s : skill_trees){
         String str = s.replaceAll("[^"+skill+"]","");
         if(skill.startsWith(str)) answer++;
      }
   ```   
   replaceAll로 skill을 제외한 문자들을 "" 공백 처리 후 startsWith로 시작하는지 확인합니다. replaceAll과 startsWith를 사용하면 상당히 간단해 집니다.   

1. # 풀이 2
   replaceAll만 사용한 경우 남은 문자열들과 skill의 문자열들 순서가 일치하는지 비교해서 구할 수 있습니다.   
   ```java
      for(int i=0 ; i<skill_trees.length ; i++){
            skill_trees[i] = skill_trees[i].replaceAll("[^"+skill+"]","");
        }

        char[] charSkill = skill.toCharArray();
        int answer = 0;
        for(String s : skill_trees){
            int cnt = 0;
            boolean chk = true;
            for(char c : s.toCharArray()){ //skill문자열 이외를 제거한 skill_trees의 횟수만큼 반복문을 돌면서 skill의 값들과 비교를 합니다.
                if(c != charSkill[cnt]){ 
                    chk = false;
                    break;
                }
                cnt++;
            }
            if(chk) answer++;
        }
        return answer;
   ```   
   skill문자열 이외를 제거한 skill_trees의 문자열은 skill의 문자열보다 같거나 작기 때문에 c != charSkill[cnt] 이러한 비교가 가능합니다.   
   c : skill문자열 이외를 제거한 skill_trees   
   charSkill : skill의 문자 배열 값   

1. # 풀이 3
   replaceAll와 startsWith를 사용하지 않고, 
   skill_trees에서 skill 문자의 갯수와 skill_trees에서 skill의 순서에 맡게 빠져나온 갯수가 일치하면 올바른 skill사용법이 됩니다.   
   ```java
      for(int i=0 ; i<skill_trees.length ; i++){
            int sCount = 0; //skill_trees에 속해있는 skill 갯수
            for(char c : skill_trees[i].toCharArray()){
                if(queue.contains(c)) ++sCount;
            }

            int count = 0; //skill에서 순서대로 빠져나온 갯수
            for(char c : skill_trees[i].toCharArray()){
                if(!queue.isEmpty()){ //CBD가 다 빠졌을 때 queue.peek()자체가 에러발생하는데 이를 방지
                    if(c == queue.peek()) {
                        queue.poll();
                        count++;
                    }
                }
            }

            if(sCount == count) answer++;

            queueMake(queue,skill); //남아있는 queue를 비우고 다시 채움
        }
        return answer;
   ```   
   