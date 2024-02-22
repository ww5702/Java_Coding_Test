```
import java.util.Arrays;
import java.util.stream.*;
class Solution {
    public boolean solution(int x) {
        int[] digits = Stream.of(String.valueOf(x).split(""))
            .mapToInt(Integer::parseInt).toArray();
        int total = Arrays.stream(digits).sum();
        
        return x % total == 0 ? true : false;
    }
}
```
