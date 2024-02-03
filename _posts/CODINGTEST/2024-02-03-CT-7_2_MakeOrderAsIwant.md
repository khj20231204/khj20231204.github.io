---
layout: single
title: 7-2 문자열 마음대로 정렬
categories: CODINGTEST
tag: []
---

1. # 문제 설명
   문자열로 구성된 리스트 strings와, 정수 n이 주어졌을 때, 각 문자열의 인덱스 n번째 글자를 기준으로 오름차순 정렬하려 합니다. 예를 들어 strings가 ["sun", "bed", "car"]이고 n이 1이면 각 단어의 인덱스 1의 문자 "u", "e", "a"로 strings를 정렬합니다.

   제한 조건   
   strings는 길이 1 이상, 50이하인 배열입니다.   
   strings의 원소는 소문자 알파벳으로 이루어져 있습니다.   
   strings의 원소는 길이 1 이상, 100이하인 문자열입니다.   
   모든 strings의 원소의 길이는 n보다 큽니다.   
   인덱스 1의 문자가 같은 문자열이 여럿 일 경우, 사전순으로 앞선 문자열이 앞쪽에 위치합니다.   

   입출력 예

   |         strings       |  n   |        return         |
   |:---------------------:|:----:|:---------------------:|
   | ["sun", "bed", "car"] |  1   | ["car", "bed", "sun"] |
   |["abce", "abcd", "cdx"]|  2   |["abcd", "abce", "cdx"]|

   입출력 예 설명   
   입출력 예 1   
   "sun", "bed", "car"의 1번째 인덱스 값은 각각 "u", "e", "a" 입니다. 이를 기준으로 strings를 정렬하면 ["car", "bed", "sun"] 입니다.   
      
   입출력 예 2   
   "abce"와 "abcd", "cdx"의 2번째 인덱스 값은 "c", "c", "x"입니다. 따라서 정렬 후에는 "cdx"가 가장 뒤에 위치합니다. "abce"와 "abcd"는 사전순으로 정렬하면 "abcd"가 우선하므로, 답은 ["abcd", "abce", "cdx"] 입니다.   

   [풀이 참고](https://discover.tistory.com/42 "풀이 참고")

1. # 풀이 
   ```java
      //문자를 앞에 붙이기
      public static String[] solution1(String[] strings, int n){
         String[] answer = new String[strings.length];

         for(int i=0 ; i<strings.length ; i++) answer[i] = strings[i].charAt(n)+strings[i];

         Arrays.sort(answer);

         for(int i=0 ; i<strings.length ; i++) answer[i] = answer[i].substring(1,answer[i].length());

         return answer;
      }

      //for문 이용 아스키코드로 정렬
      public static String[] solution2(String[] strings, int n) {
         String[] answer = new String[strings.length];

         Arrays.sort(strings);

         //65~90 97~122
         int count = 0;
         for(int i=97 ; i<=122 ; i++){
            for(int j=0 ; j<strings.length ; j++){
                  if(strings[j].charAt(n) == (char)i ){
                     answer[count++] = strings[j];
                  }
            }
         }
         return answer;
      }

      //sort재정의
      public static String[] solution3(String[] strings, int n) {

         Arrays.sort(strings);

         Arrays.sort(strings, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                  if(o1.charAt(n) > o2.charAt(n)) return 1;
                  else if(o1.charAt(n) < o2.charAt(n)) return -1;
                  return 0;
            }
         });

         return strings;
      }

      //람다
      public static String[] solution4(String[] strings, int n) {

         Arrays.sort(strings);

         Arrays.sort(strings, (o1,o2) -> {
            if (o1.charAt(n) > o2.charAt(n)) return 1;
            else if(o1.charAt(n) < o2.charAt(n)) return -1;
            return 0;
         });
         return strings;
      }
   ```
