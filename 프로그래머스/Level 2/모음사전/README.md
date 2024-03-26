```
import java.util.*;
import java.util.Arrays;
class Solution {
    List<String> list = new ArrayList<>();
    public int solution(String word) {
        String[] arr = {"A","E","I","O","U"};
        
        dfs(arr, "");
        int answer = list.indexOf(word);
        return answer;
    }
    
    public void dfs(String[] arr, String word) {
        list.add(word);
        if (word.length() == 5) { return; }
        
        for (int i = 0; i < arr.length; i++) {
            dfs(arr, word+arr[i]);
        }
    }
}
```
