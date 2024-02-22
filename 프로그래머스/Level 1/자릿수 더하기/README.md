```
import java.util.*;
class Solution {
    public long solution(long n) {
        String[] list = String.valueOf(n).split("");
        Arrays.sort(list);

        StringBuilder sb = new StringBuilder();
        for (String num : list)  {
            sb.append(num);
        }
        sb.reverse();
        return Long.parseLong(sb.toString());
    }
}
```
