```
import java.util.*;
import java.util.stream.*;
public class Solution {
    public int[] solution(int []arr) {
        List<Integer> arrlist = new ArrayList<>();
        for (int i = 0; i < arr.length; i++) {
            if (arrlist.size() == 0) {
                arrlist.add(arr[i]);
            } else {
                if (arrlist.get(arrlist.size()-1) != arr[i]) {
                    arrlist.add(arr[i]);
                }
            }
        }
        int[] answer = arrlist.stream().mapToInt(i->i).toArray();
        return answer;
    }
}
```
