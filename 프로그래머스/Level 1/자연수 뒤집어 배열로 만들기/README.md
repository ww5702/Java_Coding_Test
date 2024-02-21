StringBuilder를 바로 집어넣으니 5,4,3,2,1이 53,52,51,50,49가 되었다.   
따라서 sb -> String -> Int로 넣었다.   
```
import java.util.Arrays;
class Solution {
    public int[] solution(long n) {
        StringBuilder sb = new StringBuilder();
        sb.append(String.valueOf(n));
        sb.reverse();
        int[] answer = new int[sb.length()];
        for (int i = 0; i < sb.length(); i++) {
            answer[i] = Integer.valueOf(String.valueOf(sb.charAt(i)));
        }
        
        return answer;
    }
}
```
