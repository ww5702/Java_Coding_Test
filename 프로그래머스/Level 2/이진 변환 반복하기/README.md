```
import java.util.Arrays;
class Solution {
    public int[] solution(String s) {
        int[] answer = new int[2];
        while (!s.equals("1")) {
            int size = s.replaceAll("0","").length();
            answer[1] += s.length()-size;
            s = Integer.toBinaryString(size);
            answer[0] += 1;
        }
        //System.out.println(Arrays.toString(answer));
        return answer;
    }
}
```
