```
import java.util.Arrays;
import java.util.stream.*;
import java.util.*;

class Solution {
    public int[] solution(String[] id_list, String[] report, int k) {
        List<String> distinct_id_list = Arrays.stream(report).distinct().collect(Collectors.toList());
        //System.out.println(distinct_id_list.toString());
        HashMap<String, Integer> list = new HashMap<>();
        for (String str: distinct_id_list) {
            String[] value = str.split(" ");
            list.put(value[1], list.getOrDefault(value[1], 0) + 1);
        }
        //System.out.println(list);
        int[] answer = new int[id_list.length];
        for (String str: distinct_id_list) {
            String[] value = str.split(" ");
            int num = list.get(value[1]);
            if (num >= k) {
                int idx = Arrays.asList(id_list).indexOf(value[0]);
                answer[idx] += 1;
            }
        }
        return answer;
    }
}
```
