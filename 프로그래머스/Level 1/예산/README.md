```
import java.util.Arrays;
class Solution {
    public int solution(int[] d, int budget) {
        int answer = 0;
        Arrays.sort(d);
        //System.out.println(Arrays.toString(d));
        for (int i = 0; i < d.length; i++) {
            if (budget >= d[i]) {
                answer += 1;
                budget -= d[i];
            }
        }
        return answer;
    }
}
```
