```
import java.util.Arrays;
import java.util.*;
class Solution {
    public int solution(int k, int[] tangerine) {
        int answer = 0;
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int t : tangerine) {
            map.put(t, map.getOrDefault(t, 0) + 1);
        }
        //System.out.println(map);
        List<Integer> list = new ArrayList<>(map.keySet());
        list.sort((o1, o2) -> map.get(o2)-map.get(o1));
        //System.out.println(list.toString());
        for (Integer idx : list) {
            //System.out.println(idx);
            k -= map.get(idx);
            answer += 1;
            if (k <= 0) { break; }
        }
        
        return answer;
    }
}
```
