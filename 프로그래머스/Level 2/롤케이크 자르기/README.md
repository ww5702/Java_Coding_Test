반복문 하나를 돌면서 set와 map을 이용해 풀이   

```
import java.util.Arrays;
import java.util.*;

class Solution {
    public int solution(int[] topping) {
        int answer = 0;
        HashSet<Integer> setA = new HashSet<Integer>();
        HashSet<Integer> setB = new HashSet<Integer>();
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int top : topping) {
            map.put(top, map.getOrDefault(top, 0) + 1);
            setB.add(top);
        }
        for (int t : topping) {
            setA.add(t);
            map.put(t, map.get(t) - 1);
            
            if (map.get(t) == 0) {
                setB.remove(t);
            }
            answer += setA.size() == setB.size() ? 1 : 0;
        }
        
        return answer;
    }
}
```
