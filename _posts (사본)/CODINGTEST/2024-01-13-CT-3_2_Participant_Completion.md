---
layout: single
title: 3-2 완주하지 못한 선수
categories: CODINGTEST
tag: []
---

1. # 문제 설명
   수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

   마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

   제한사항
   마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
   completion의 길이는 participant의 길이보다 1 작습니다.
   참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
   참가자 중에는 동명이인이 있을 수 있습니다.   
   
   입출력 예   

   |                   participant                   |                completion              | return |
   |:-----------------------------------------------:|:--------------------------------------:|:------:|
   |         ["leo", "kiki", "eden"]                 |              ["eden", "kiki"]	       |"leo"|
   |["marina", "josipa", "nikola", "vinko", "filipa"]|["josipa", "filipa", "marina", "nikola"]|"vinko"|
   |    ["mislav", "stanko", "mislav", "ana"]        |      ["stanko", "ana", "mislav"]       |"mislav"|

   입출력 예 설명
   
   예제 #1
   "leo"는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

   예제 #2
   "vinko"는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

   예제 #3
   "mislav"는 참여자 명단에는 두 명이 있지만, 완주자 명단에는 한 명밖에 없기 때문에 한명은 완주하지 못했습니다.

1. # 풀이
   participant배열에서 completion배열 값을 제거하는데 결과는 무조건 participant 인원이 한 명만 남는다는 것입니다.(이 조건 때문에 난이도가 확 낮아짐)   
   
   1) map이용   
   키값으로 참가자명만 집어넣는 경우 map의 key는 중복을 제거하기 때문에, 동명이인의 경우 정확한 값이 저장이 안 됩니다. 그렇기 때문에 동명이인이 나올 때마다 vlues의 숫자를 증가 시킵니다.   
   ```java
      public String solution(String[] participant, String[] completion) {        
        HashMap<String, Integer> map = new HashMap<>();
        for(String s : participant){
            map.put(s, map.getOrDefault(s,0)+1); //기본값을 1로 설정, 동명이인이 나올 때 마다 1씩 증가
        }
        
        for(String s : completion){
            int num = map.get(s) - 1;  //completion의 value를 가져와서 -1을 한 후 그 값이 0 이면 완주를 했다는 의미
            if(num == 0){
                map.remove(s);
            }else map.put(s,num);
        }
   ```   
   
   2) list이용   
   list.add 후 completion을 반본문으로 돌면서 해당 선수 이름을 remove합니다.   
   ```java  
      ArrayList<String> list = new ArrayList<>();
      for(String s : participant){list.add(s);}

      for(String s : completion){list.remove(s);}//<--- 효율성 초과
      System.out.println(list.get(0));
      
      return map.keySet().iterator().next();
    }
   ```   
   remove를 수행할 때 list는 배열처럼 인덱스로 바로 접근을 하는 것이 아니라 첫번째 값에서 해당값까지 헤더와 테일로 연결된 값들을 전부 탐색하기 때문에 시간복잡도가 O(n)이 됩니다. 반복문 안에서 수행하기 때문에 최종 복잡도는 O(n²)이 되기 때문에 효율성 검사에서 통과를 못 합니다.   

   3) 배열이용   
   ```java
      //비교할 값 2개를 먼저 정렬
      Arrays.sort(participant); 
      Arrays.sort(completion);

      for(int i=0 ; i<completion.length ; i++){
         if(!participant[i].equals(completion[i])){  //정렬 후 비교하는데 만약 일치하지 않으면
               return participant[i]; //일치하지 않는 이름을 바로 리턴 - 완주하지 못한 인원이 단 1명이기 때문에 가능
         }
      }

      return participant[participant.length-1];
   ```

