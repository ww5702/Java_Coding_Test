```
import java.util.HashMap;
import java.util.*;
class Solution {
    public int[][] solution(int[][] data, String ext, int val_ext, String sort_by) {
        int[][] answer = {};
        HashMap<String, Integer> value = new HashMap<String, Integer>();
        value.put("code",0);
        value.put("date",1);
        value.put("maximum",2);
        value.put("remain",3);
        
        List<int[]> filtered = new ArrayList<>();
        for (int[] d : data) {
            if (d[value.get(ext)] < val_ext) {
                filtered.add(d);
            }
        }
        filtered.sort(Comparator.comparingInt(arr -> arr[value.get(sort_by)]));
        
        return filtered.toArray(new int[0][]);
    }
}
```
