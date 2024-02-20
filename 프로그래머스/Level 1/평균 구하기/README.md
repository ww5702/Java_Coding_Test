```
import java.util.Arrays;
class Solution {
    public double solution(int[] arr) {
        return Double.valueOf(Arrays.stream(arr).sum())/arr.length;
    }
}
```
