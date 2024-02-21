```
import java.util.*;
import java.util.Arrays;
import java.util.stream.*;

public class Solution {
    public int solution(int n) {
        int[] answer = Stream.of(String.valueOf(n).split("")).mapToInt(Integer::parseInt).toArray();
        //System.out.println(Arrays.toString(answer));
        return Arrays.stream(answer).sum();
    }
}
```
