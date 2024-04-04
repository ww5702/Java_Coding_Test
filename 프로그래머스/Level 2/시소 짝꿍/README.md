정렬을 이용해 큰 수로 순환하도록 바꾼다.   
비율은 1,1 / 2,3 / 2,4 / 3,4 만 남게 된다.   
4,3 이나 3,2는 정렬을 했기 때문에 계산할 필요가 없다.   
180 x 3 = 270 x 2인데   
270 x 2 = 180 x 3과 같다.   
2,4 는 1,2와 비율이 같다.   
따라서 4가지 경우만 존재하는지 검색해본다.   
없다면 map+1   
100,180,360,100,270	의 경우   
100 = 2, 180 = 1, 270 = 1로 존재할때   
360의 1,1 1,2 2,3 3,4를 구해본다.   
360,180,240,270이 값으로 나오고   
map에 180 270이 존재하므로 2가 추가 된다.   

```
import java.util.*;
import java.util.Arrays;
class Solution {
    public long solution(int[] weights) {
        long answer = 0;
        Arrays.sort(weights);
        Map<Double, Integer> map = new HashMap<>();
        int[] list = {2,3,4};
        for (int w : weights) {
            double a = w*1.0;
            double b = (w*2.0)/3.0;
            double c = (w*1.0)/2.0;
            double d = (w*3.0)/4.0;
            if(map.containsKey(a)) answer += map.get(a);
            if(map.containsKey(b)) answer += map.get(b);
            if(map.containsKey(c)) answer += map.get(c);
            if(map.containsKey(d)) answer += map.get(d);
            map.put((w*1.0), map.getOrDefault((w*1.0), 0)+1);
            //System.out.println(map);
        }
        return answer;
    }
}
```
