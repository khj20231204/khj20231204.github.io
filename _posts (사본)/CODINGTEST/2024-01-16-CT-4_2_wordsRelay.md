---
layout: single
title: 4-2 끝말 잇기
categories: CODINGTEST
tag: []
---

1. # 문제 설명
    입력되는 단어가 순서대로 배치될 때 끝말잇기로 끝까지 이어지는지 확인하세요.
    끝말잇기는 사용했던 단어가 다시 사용되면 안됩니다.
    단어의 첫 글자는 앞 단어의 마지막 글자로 시작되어야 합니다.
    (단, 첫 단어의 첫 글자는 확인하지 않습니다.)

    입력1: ["tank", "kick", "know", "wheel", "land", "dream"]
    출력1: true

    단어의 연결이 모두 이어지고, 중복되는 단어가 없었습니다.

    입력2: ["tank", "kick", "know", "wheel", "land", "dream", "mother", "robot", "tank"]
    출력2: false

    사용되었던 tank 단어가 다시 사용되었습니다.

1. # 풀이   
    끝말잇기 검색을 하는 알고리즘을 짜야합니다. 중복을 제거한 후 앞 단어의 끝 글자와 뒷 단어의 첫 글자가 같으면 끝말잇기가 가능합니다. 다음 2가지를 체크해야 합니다.      
    1)중복 제거 후 단어 갯수 일치 여부   
    2)앞 단어 끝 글자와 뒷 단어 첫 글자의 비교   

    주의 할 점은 중복을 제거하는 거기 때문에 set을 사용하면 되는데 set을 사용함에 있어서 set은 출력시 순서가 보장되어 있지 않기 때문에 중복제거한 문자열을 set에 저장 후 단어를 비교하면 안 된다는 점입니다. 즉, set을 이용하지 않고 중복을 제거 후 단어비교 / 단어 비교 후 set으로 중복 제거 이렇게 나뉠 수 있습니다.

1. # set을 이용하지 않고 중복 제거 후 단어 비교
    
    1)중복제거는 stream으로 합니다.   
    
    스트림 배열 생성 -> 중복 제거 -> 배열로 변환 -> 원본 배열과 갯수 확인   

    ```java
    public boolean solution(String[] words) {
        String[] convertWords = Arrays.stream(words).distinct().toArray(String[]::new);
            if(convertWords.length != words.length){
            return false;
        }
    }
    ```   
    stream으로 중복 제거 후 다시 convertWords 문자열 배열로 저장. 원본 배열과 갯수가 다르면 false리턴   

    2)단어 비교   
    ```java
        char[] charArr = words[0].toCharArray();
        char tail = charArr[charArr.length-1]; //앞 단어 끝 글자 입력
        //또는
        tail = wordsl.charAt(0);  //charAt으로 바로 0번째의 한 문자를 가져올 수 있습니다.

        for(int i=1 ; i<words.length ; i++){
            charArr = words[i].toCharArray();
            
            if(tail == charArr[0]){
                tail = charArr[charArr.length-1];                
            }else
                return false;
            }
            
        return true;
    ```   
    toCharArray()는 문자열을 char배열로 변환하고, charAt(idx)는 문자열의 idx번째 문자를 바로 가져올 수 있습니다.(idx는 0부터 시작)   
    tail은 앞 문자열의 끝 문자고, charArr[0]은 다음 문자열의 첫 문자가 됩니다.

1. # Set을 사용해서 문자열 비교 후 Set에 저장해서 중복 확인
    Set의 성질을 이용해서 문자열의 비교 후 끝말잇기가 성립되면 Set에 저장 후 최종 Set에 저장된 갯수와 문자열의 갯수가 같으면 중복이 없다는 의미가 됩니다.   
    
    -앞 문자열의 끝 문자와 다음 문자열의 첫 문자 확인 후 Set에 저장
    ```java
        public boolean solution(String[] words) {
            
            Set<String> set = new HashSet<>();
            
            char headTail = words[0].charAt(0); //최초 첫 글자를 입력하기 위해서 임의로 첫 글자의 첫 문자로 셋팅
            for(String s : words){
                if(headTail == s.charAt(0)){ //비교하는 다음 문자열의 첫 문자
                    set.add(s);
                    headTail = s.charAt(s.length()-1);  //입력하는 건 다음 문자열의 끝 문자
                }
                return false;
            }
            
            return set.size() == words.length;  //여기서 중복 확인 여부 체크
        }
    ```   
    

