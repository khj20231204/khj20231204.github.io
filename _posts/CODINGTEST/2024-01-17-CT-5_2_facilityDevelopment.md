---
layout: single
title: 5-2 기능 개발
categories: CODINGTEST
tag: []
---

1. # 문제 설명
   프로그래머스 팀에서는 기능 개선 작업을 수행 중입니다. 각 기능은 진도가 100%일 때 서비스에 반영할 수 있습니다.

   또, 각 기능의 개발속도는 모두 다르기 때문에 뒤에 있는 기능이 앞에 있는 기능보다 먼저 개발될 수 있고, 이때 뒤에 있는 기능은 앞에 있는 기능이 배포될 때 함께 배포됩니다.

   먼저 배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses와 각 작업의 개발 속도가 적힌 정수 배열 speeds가 주어질 때 각 배포마다 몇 개의 기능이 배포되는지를 return 하도록 solution 함수를 완성하세요.

   제한 사항   
   작업의 개수(progresses, speeds배열의 길이)는 100개 이하입니다.   
   작업 진도는 100 미만의 자연수입니다.   
   작업 속도는 100 이하의 자연수입니다.   
   배포는 하루에 한 번만 할 수 있으며, 하루의 끝에 이루어진다고 가정합니다.    예를 들어 진도율이 95%인 작업의 개발 속도가 하루에 4%라면 배포는 2일 뒤에 이루어집니다.   

   입출력 예

   |        progresses      |       speeds     |  return |
   |:----------------------:|:----------------:|:-------:|
   |      [93, 30, 55]      |    [1, 30, 5]    | [2, 1]  |
   |[95, 90, 99, 99, 80, 99]|[1, 1, 1, 1, 1, 1]|[1, 3, 2]|

   입출력 예 설명   

   입출력 예 #1   
   첫 번째 기능은 93% 완료되어 있고 하루에 1%씩 작업이 가능하므로 7일간 작업 후 배포가 가능합니다.   
   두 번째 기능은 30%가 완료되어 있고 하루에 30%씩 작업이 가능하므로 3일간 작업 후 배포가 가능합니다. 하지만 이전 첫 번째 기능이 아직 완성된 상태가 아니기 때문에 첫 번째 기능이 배포되는 7일째 배포됩니다.   
   세 번째 기능은 55%가 완료되어 있고 하루에 5%씩 작업이 가능하므로 9일간 작업 후 배포가 가능합니다.   

   따라서 7일째에 2개의 기능, 9일째에 1개의 기능이 배포됩니다.

   입출력 예 #2   
   모든 기능이 하루에 1%씩 작업이 가능하므로, 작업이 끝나기까지 남은 일수는 각각 5일, 10일, 1일, 1일, 20일, 1일입니다. 어떤 기능이 먼저 완성되었더라도 앞에 있는 모든 기능이 완성되지 않으면 배포가 불가능합니다.   

   따라서 5일째에 1개의 기능, 10일째에 3개의 기능, 20일째에 2개의 기능이 배포됩니다.   

1. # 풀이 - ArrayList이용
   ```java
      //1.(100-progress / speeds)를 올림한 결과 list
      //2.계산 결과 list를 배포하는 list
      //3.배포 list를 배열로 변경

      //1. (100-progress / speeds)를 올림한 결과 calList
      List<Integer> calList = new ArrayList<>();
      int cnt = 0;
      for(int i : progresses){
         float a = ((float)(100-i)/(float)speeds[cnt++]);
         //(float)(100-i)/speeds[cnt++]; 또는 (100-i)/(float)speeds[cnt++];
         //제수와 피제수 중 하나만 float으로 변환해도 결과는 float가 됨.
         int b = (int)Math.ceil(a);
         //System.out.println(b);
         calList.add(b);
      }

      //2. 배포 List 생성 - resultList
      //앞에서 수(head)가 더 크면 count를 증가 시키고, 더 작으면 count를 list에 입력 후 현재 값(next)을 head에 입력
      List<Integer> resultList = new ArrayList<>();
      int count = 1;
      int head = calList.remove(0); //최초 비교할 값 입력

      Iterator iter = calList.iterator();
      while(iter.hasNext()){
         int next = (int)iter.next();
         if(head >= next){ //앞에 수가 더 크면 count++;
            count++;
         }else{
            resultList.add(count);
            count = 1;
            head = next;
         }
      }
      resultList.add(count);

      //3. resultList를 배열로 변경
      return resultList.stream().mapToInt(Integer::intValue).toArray();
   ```   
   float a = ((float)(100-i)/(float)speeds[cnt++]);   
   결과를 float으로 받아야 솟수점 숫자가 남게 되고 올림이 가능해집니다. 만약 (100-i)/speeds[cnt++]; 제수나 피제수를 float으로 변화하지 않으면 결과가 3.333이 나오더라도 /(나머지 연사자)가 자동 int형으로 변환해서 3이 나오게 됩니다. 즉, 나눠주는 값들을 float으로 변환하지 않으면 대입한 결과 a는 float형이기 때문에 3.333의 올림 값으로 3.0이란 값이란 잘못된 값이 나오게 됩니다..

1. # 풀이 - Queue이용
   ```java
      //완료 날 계산
      Queue<Integer> queue = new LinkedList<>(); 
      int idx = 0;
      for(int i : progresses){
         float remainDayF = (100-i)/(float)speeds[idx++];
         queue.offer((int)Math.ceil(remainDayF));
      }

      //배포 날 카운트
      Queue<Integer> distriQueue = new LinkedList<>();
      int head = queue.poll();
      int count = 1;
      int max = queue.size();
      while(!queue.isEmpty()){
         int rear = queue.poll();
         
         if(head < rear){ //입력
               distriQueue.offer(count);
               count = 1;
               head = rear;
         }else {  //카운트 증가
               count++;
         }
      }
      distriQueue.offer(count);

      //리스트의 배포 날을 배열로 변환 후 리턴 
      return distriQueue.stream().mapToInt(Integer::intValue).toArray();
   ```   
   List를 이용했을 때와 마찬가지로 똑같이 3단계로 생각합니다. Queue는 List와 다르게 값을 꺼내면 자체 size가 줄어들기 때문에 iterator를 생성하지 않고 바로 isEmpty()로 while문을 사용합니다. 하지만 전체 알고리즘은 똑같습니다.   
   Queue역시 List처럼 Collelctions인터페이스를 상속받았기 때문에 isEmpty(), size(), clear(), contains() 등 컬렉션 프레임워크의 대부분 메소드가 사용가능합니다. iterator()역시 사용가능합니다.   