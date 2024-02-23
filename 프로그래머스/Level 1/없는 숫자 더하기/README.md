```
import java.util.Arrays;
class Solution {
    public int solution(int[] numbers) {
        int sum = Arrays.stream(numbers).sum();
        return 45-sum;
    }
}
```
