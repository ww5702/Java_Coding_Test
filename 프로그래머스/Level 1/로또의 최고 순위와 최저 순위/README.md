```
import java.util.Arrays;
import java.util.*;
class Solution {
    public int[] solution(int[] lottos, int[] win_nums) {
        Set<Integer> lottoSet = new HashSet<>();
        for (int lotto : lottos) if(lotto != 0) lottoSet.add(lotto);
        int[] answer = {1 + lottoSet.size(), 7};
        for (int win_num : win_nums) if(lottoSet.contains(win_num)) { --answer[0]; --answer[1]; }
        if(answer[0] == 7) --answer[0];
        if(answer[1] == 7) --answer[1];
        return answer;
    }
}
```
