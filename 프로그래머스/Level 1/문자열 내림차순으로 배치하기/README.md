```
import java.util.*;
class Solution {
    public String solution(String s) {
        char[] arr = s.toCharArray();
        Arrays.sort(arr);
        StringBuilder sb = new StringBuilder();
        sb.append(arr).reverse();
        return sb.toString();
    }
}
```
