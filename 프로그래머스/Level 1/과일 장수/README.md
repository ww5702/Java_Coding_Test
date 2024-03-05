```
import java.util.Arrays;
import java.util.*;
class Solution {
    public int solution(int k, int m, int[] score) {
        int answer = 0;
        Integer[] newarr = Arrays.stream(score).boxed().toArray(Integer[]::new);
        Arrays.sort(newarr, Collections.reverseOrder());
        //System.out.println(Arrays.toString(newarr));
        for (int i = 0; i < score.length; i+=m) {
            if (i + m > score.length) { break; }
            Integer[] temp = Arrays.copyOfRange(newarr, i, i+m);
            int price = temp[temp.length-1];
            answer += (price * m);
        }
        return answer;
    }
}
```
