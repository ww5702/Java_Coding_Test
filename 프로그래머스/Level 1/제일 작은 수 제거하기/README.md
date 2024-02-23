```
import java.util.Arrays;
class Solution {
    public int[] solution(int[] arr) {
        int min = Arrays.stream(arr).min().getAsInt();
        int[] answer = Arrays.stream(arr)
            .filter(i -> i != min)
            .toArray();
        if (answer.length == 0) {
            answer = new int[] {-1};
        }
        return answer;
    }
}
```
