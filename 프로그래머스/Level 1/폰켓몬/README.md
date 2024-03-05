```
import java.util.*;
class Solution {
    public int solution(int[] nums) {
        HashSet<Integer> set = new HashSet<Integer>();
        for (int num : nums) {
            set.add(num);
        }
        return nums.length/2 <= set.size() ? nums.length/2 : set.size();
    }
}
```
