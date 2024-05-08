효율성도 있는 문제이고 원소들의 값이 2억이 넘으므로   
이분탐색으로 진행해준다.   

```
import java.util.Arrays;
class Solution {
    public int solution(int[] stones, int k) {
        int start = 0, end = Arrays.stream(stones).max().getAsInt();
        
        while(start <= end) {
            int middle = (start + end)/2;
            int jump = k;
            boolean canGo = true;
            for (int stone : stones) {
                if (stone - middle >= 0) {
                    jump = k;
                } else {
                    jump -= 1;
                    if (jump <= 0) {
                        canGo = false;
                        break;
                    }
                }
            }
            
            if (canGo) {
                start = middle+1;
            } else {
                end = middle-1;
            }
            
        }
        
        //System.out.println(start+" "+end);
        return end;
    }
}
```
