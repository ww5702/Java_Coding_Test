```
import java.util.*;
import java.util.Arrays;
class Solution {
    
    public int solution(String[] want, int[] number, String[] discount) {
        int answer = 0;
        ArrayList<String> list = new ArrayList<>();

        for (int i=0; i<want.length; i++) {
            while (number[i]-- > 0) {
                list.add(want[i]);
            }
        }

        for (int i=0; i<discount.length-list.size()+1;i ++) {
            ArrayList<String> l = (ArrayList<String>) list.clone();
            for (int j=i; j<i+list.size(); j++) {
                if (l.contains(discount[j])) {
                    l.remove(discount[j]);
                } else {
                    break;
                }
            }
            answer += l.size()==0 ? 1 : 0;
        }

        return answer;
    }
    
}
```
