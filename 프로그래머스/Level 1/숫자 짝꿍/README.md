```
import java.util.Arrays;
import java.util.*;
class Solution {
    public String solution(String X, String Y) {
        String answer = "";
        String[] Xarr = X.split("");
        String[] Yarr = Y.split("");
        List<Integer> list = new ArrayList<>();
        for (int i = 0; i <= 9; i++) {
            long num = i;
            long xnum = Arrays.stream(Xarr)
                .filter(n -> Long.parseLong(n) == num)
                .count();
            long ynum = Arrays.stream(Yarr)
                .filter(n -> Long.parseLong(n) == num)
                .count();
            
            for (int j = 0; j < Math.min(xnum,ynum); j++) {
                list.add(i);
            }
        }
        Collections.sort(list, Collections.reverseOrder());
        if (list.size() < 1) { return "-1"; }
        
        String num = "";
        for (long i: list) {
            num += i;
        }
        if (num.charAt(0) == '0') {
            return "0";
        } else {
            return num;
        }
    }
}
```
