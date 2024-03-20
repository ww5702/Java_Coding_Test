LRU알고리즘 사용   

```
import java.util.*;
import java.util.Arrays;
class Solution {
    public int solution(int cacheSize, String[] cities) {
        int answer = 0;
        if (cacheSize == 0) {
            return cities.length * 5;
        }
        List<String> cache = new ArrayList<>();
        for (int i = 0; i < cities.length; i++) {
            String city = cities[i].toLowerCase();
            // miss
            if (!cache.contains(city)) {
                answer += 5;
                if (cache.size() >= cacheSize) {
                    cache.remove(0);
                }
                cache.add(city);
                //System.out.println(cache.toString());
                continue;
            }
            
            if (cache.contains(city)) {
                cache.remove(city);
                cache.add(city);
                //System.out.println(cache.toString());
                answer += 1;
            }
            
            
        }
        return answer;
    }
}
```
