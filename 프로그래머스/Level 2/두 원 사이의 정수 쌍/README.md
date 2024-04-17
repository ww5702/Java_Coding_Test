4분면까지의 있으므로 하나만 구해서 *4를 해준다.   
x^2 + y^2 = r^2 공식을 이용한다.   
```
import java.util.*;
class Solution {
    public long solution(int r1, int r2) {
        long answer = 0;
        for (int i = 1; i <= r2; i++) {
            int start = (int) Math.ceil(Math.sqrt((long) r1 * r1 - (long) i * i));
            int end = (int) Math.floor(Math.sqrt((long) r2 * r2 - (long) i * i));
            answer += end - start + 1;
        }
        return answer*4;
    }
}
```
