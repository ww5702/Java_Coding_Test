```
import java.util.*;
class Solution {
    public int[] solution(int[] sequence, int k) {
        
        int left = 0, right = -1, sum = 0;
        int sLeft = 0, sRight = 0, length = 1000001;
        while (right < sequence.length) {
            if (sum < k) {
                if (++right < sequence.length) {
                    sum += sequence[right];
                }
            } else if (k < sum) {
                sum -= sequence[left++];
            } else {
                if (right - left < length) {
                    length = right - left;
                    sLeft = left;
                    sRight = right;
                }
                sum -= sequence[left++];
            }
        }
        int[] answer = {sLeft,sRight};
        return answer;
    }
}
```
