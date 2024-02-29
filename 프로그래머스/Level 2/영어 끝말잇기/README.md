```
import java.util.*;
class Solution {
    public int[] solution(int n, String[] words) {
        int[] answer = new int[2];
        List<String> wordList = new ArrayList<>();
        wordList.add(words[0]);
        
        int turn = 1;
        String lastWord = wordList.get(wordList.size()-1);
        String lastWordStart = lastWord.substring(lastWord.length()-1, lastWord.length());
        
        for (int i = 1; i < words.length; i++) {            
            //System.out.println(words[i]);
            String cur = words[i];
            // 끝말잇기
            if (cur.startsWith(lastWordStart) && !wordList.contains(words[i])) {
                wordList.add(words[i]);
                lastWord = wordList.get(wordList.size()-1);
                lastWordStart = lastWord.substring(lastWord.length()-1, lastWord.length());
            } else {
                //System.out.println("x");
                answer[0] = (i+1)%n == 0 ? n : (i+1)%n;
                answer[1] = turn;
                break;
            }
            
            if ((i+1) % n == 0) {
                turn += 1;
            }
        }
        
        return answer;
    }
}
```
