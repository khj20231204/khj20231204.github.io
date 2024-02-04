---
layout: single
title: 7-3 JadenCase
categories: CODINGTEST
tag: []
---

1. # 문제 설명
   JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 단, 첫 문자가 알파벳이 아닐 때에는 이어지는 알파벳은 소문자로 쓰면 됩니다. (첫 번째 입출력 예 참고)
   문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.

   제한 조건   
   s는 길이 1 이상 200 이하인 문자열입니다.   
   s는 알파벳과 숫자, 공백문자(" ")로 이루어져 있습니다.   
   숫자는 단어의 첫 문자로만 나옵니다.   
   숫자로만 이루어진 단어는 없습니다.   
   공백문자가 연속해서 나올 수 있습니다.   

   입출력 예   

   |           s             |          return         |
   |:-----------------------:|:-----------------------:|
   | "3people unFollowed me" | "3people Unfollowed Me" |
   |   "for the last week"   |   "For The Last Week"   |

1. # 풀이
   ```java
      public String solution(String s) {
         String answer = "";
         
         s = s.toLowerCase();
         
         char[] charArr = new char[s.length()];
         
         char before = ' ';
         int cnt = 0;
         for(char c : s.toCharArray()){
            if(before == ' ') c = Character.toUpperCase(c);
                  
            charArr[cnt++] = c;
            before = c;
         }
         
         answer = String.valueOf(charArr);

         return answer;
      }
   ```   
   "앞에 문자가 공백이면 뒤에 문자를 대문자로 한다" 이 부분을   
   1) if(i == ' ') charArr[i+1] = c;   
   2) before = 앞에 문자 , if(before = ' ') charArr[ i ] = c;   
   현재 공백이면 i+1 번째에 대문자를 입력할 수 있고, 앞문자를 변수에 넣고 앞문자가 공백이면 현재 위치에 대문자를 입력할 수 있습니다.   
   1)번 같은 경우 현재 루프를 돌고 있는 위치는 i 인데 i+1 번째에 값을 대입하는 것이기 때문에 안정성에 문제가 생길 수 있습니다.   
   2)번은 조건 검색은 앞 문자로 하고, 현재 인덱스 위치에 값을 대입하는 것이기 때문에 1)보다 안정적입니다.   
