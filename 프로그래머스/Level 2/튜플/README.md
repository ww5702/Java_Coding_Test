```
import java.util.*;
class Solution {
    public int[] solution(String s) {
        s = s.replaceAll("[}{]","");
        String[] words = s.split(",");
        HashMap<String, Integer> map = new HashMap<>();
        //System.out.println(Arrays.toString(words));
        for (String word : words) {
            map.put(word, map.getOrDefault(word, 0) + 1);
        }
        //System.out.println(map);
        List<String> keySet = new ArrayList<>(map.keySet());
        keySet.sort((o1, o2) -> map.get(o2).compareTo(map.get(o1)));
        int[] answer = new int[keySet.size()];
        for (int i = 0; i < keySet.size(); i++) {
            answer[i] = Integer.valueOf(keySet.get(i));
        }
        
        return answer;
    }
}
```
