
import java.util.*;
import java.util.stream.Collectors;

class Solution {
    public boolean solution(String[] words) {
        boolean answer = true;
        
        //배열 -> set -> 배열 -> char
        Set<String> set = Arrays.stream(words).collect(Collectors.toSet());
        System.out.println(set.size());
        
        String[] converWords = set.stream().toArray(String[]::new);
        
        char head;
        char tail;
        for(int i=0 ; i<converWords.length ; i++){
            char[] c = converWords[i].toCharArray();
            
            head = c[0];
            tail = c[c.length-1];
            
            System.out.println(converWords[i]+" ,head:"+head+" ,tail:"+tail);
        }
        
        return answer;
    }
}