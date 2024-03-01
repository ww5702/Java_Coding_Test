```
import java.util.Arrays;
class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];
        for (int i = 0; i < commands.length; i++) {
            int cur[] = commands[i];
            int start = cur[0]-1;
            int end = cur[1];
            int goal = cur[2]-1;
            int[] tempArr = Arrays.copyOfRange(array,start,end);
            Arrays.sort(tempArr);
            //System.out.println(Arrays.toString(tempArr));
            answer[i] = tempArr[goal];
        }
        return answer;
    }
}
```
