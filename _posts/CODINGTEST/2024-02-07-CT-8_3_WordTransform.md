---
layout: single
title: 8-3 단어 변환
categories: CODINGTEST
tag: []
---

1. # 문제 설명
   두 개의 단어 begin, target과 단어의 집합 words가 있습니다. 아래와 같은 규칙을 이용하여 begin에서 target으로 변환하는 가장 짧은 변환 과정을 찾으려고 합니다.

   1.한 번에 한 개의 알파벳만 바꿀 수 있습니다.   
   2.words에 있는 단어로만 변환할 수 있습니다.   
   예를 들어 begin이 "hit", target가 "cog", words가 ["hot","dot","dog","lot","log","cog"]라면 "hit" -> "hot" -> "dot" -> "dog" -> "cog"와 같이 4단계를 거쳐 변환할 수 있습니다.

   두 개의 단어 begin, target과 단어의 집합 words가 매개변수로 주어질 때, 최소 몇 단계의 과정을 거쳐 begin을 target으로 변환할 수 있는지 return 하도록 solution 함수를 작성해주세요.

   제한사항   
   각 단어는 알파벳 소문자로만 이루어져 있습니다.   
   각 단어의 길이는 3 이상 10 이하이며 모든 단어의 길이는 같습니다.   
   words에는 3개 이상 50개 이하의 단어가 있으며 중복되는 단어는 없습니다.   
   begin과 target은 같지 않습니다.   
   변환할 수 없는 경우에는 0를 return 합니다.   

   입출력 예

   |  begin | target |                        words               | return|
   |:------:|:------:|:------------------------------------------:|:-----:|
   | "hit"  |  "cog" | ["hot", "dot", "dog", "lot", "log", "cog"] |   4   |
   | "hit"  |  "cog" |     ["hot", "dot", "dog", "lot", "log"]    |   0   |

   입출력 예 설명   
   
   예제 #1   
   문제에 나온 예와 같습니다.   

   예제 #2   
   target인 "cog"는 words 안에 없기 때문에 변환할 수 없습니다.   

1. # 풀이
   ```java

   class Solution {
      
      class Word{
         String word;
         int depth;
         
         Word(String w, int d){word=w; depth=d;}
      }
      
      public int solution(String begin, String target, String[] words) {
         
         if(!Arrays.asList(words).contains(target)) return 0;   // --- ㉠
         
         Word w = new Word(begin, 0);
         Queue<Word> q = new LinkedList<>();
         q.offer(w);   // --- ㉡
         
         List<String> list = new ArrayList<>();
         
         while(!q.isEmpty()){
               w = q.poll();
               
               if(w.word.equals(target)) return w.depth;
               
               for(String s : words){
                  if(!changeable(w.word, s)) continue;   // --- ㉢
                  if(list.contains(s)) continue;   // --- ㉣
                  
                  q.offer(new Word(s, w.depth+1));
                  list.add(s);
               }
         }
         return 0;
      }
      
      boolean changeable(String s1, String s2){
         if (s1.length() != s2.length()) return false;
         
         int cnt = 0;
         for(int i=0 ; i<s1.length() ; i++){
               if(s1.charAt(i) != s2.charAt(i)) cnt++;
         }  
         return cnt == 1;
      }
   }
   ```   
   ㉠ : Arrays.asList(words).contains(target) : 배열을 List로 바꿔 target의 존재 유무만 확인.   
   또는 Arrays.stream(words).filter(w -> w.equals(target)).collect(Collectors.toList());   
   필터를 이용해서 list로 바꾼 후 list.size()가 1인가를 확인해서 구할 수 있습니다.   
   
   ㉡ : q.offer(new Word(begin, 0)) Queue에 new Words를 바로 입력합니다.   

   ㉢ : changeable함수는 현재 문자열과 1개 문자 차이로 입력할 수 있는 문자열을 찾습니다.   

   ㉣ : 한번 탐색한 문자열은 다시 탐색할 필요가 없기 때문에 list에 탐색한 문자열을 입력해서 contains로 확인합니다.   

