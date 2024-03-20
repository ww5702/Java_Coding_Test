```
import java.util.*;
class Solution {
    public int solution(String[][] clothes) {
        int answer = 1;
        HashMap<String, Integer> list = new HashMap<>();
        for (String[] cloth : clothes) {
            list.put(cloth[1], list.getOrDefault(cloth[1], 0) + 1);
        }
        //System.out.println(list);
        Iterator<Integer> it = list.values().iterator();
        while(it.hasNext()) {
            answer *= it.next().intValue()+1;
            //System.out.println(answer);
        }
        return answer-1;
    }
}
```
