```
import java.util.*;
class Solution {
    public String solution(String[] cards1, String[] cards2, String[] goal) {
        List<String> c1 = new ArrayList<String>(Arrays.asList(cards1));
        List<String> c2 = new ArrayList<String>(Arrays.asList(cards2));
        
        String answer = "Yes";
        for (String word : goal) {
            if (c1.size() >= 1) {
                if (c1.get(0).equals(word)) {
                    c1.remove(0);
                    continue;
                }
            } 
            if (c2.size() >= 1) {
                if (c2.get(0).equals(word)) {
                    c2.remove(0);
                    continue;
                }
            }
            answer = "No";
            break;
            
        }
        return answer;
    }
}
```
