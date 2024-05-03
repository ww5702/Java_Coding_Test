dp 문제이다.   
첫번째 스티커를 뜯을지 안뜯을지 두 경우로 나누어 반복문을 진행한다.   
점화식은 dp[i] = Math.max(dp[i-2]+sticker[i], dp[i-1])이다.   

```
import java.util.Arrays;
class Solution {
    public int solution(int sticker[]) {
        if (sticker.length <= 2) { return Arrays.stream(sticker).max().getAsInt(); }
        int[] dp1 = new int[sticker.length];
        int[] dp2 = new int[sticker.length];
        // 첫번째 스티커를 뜯었을 경우
        dp1[0] = sticker[0];
        dp1[1] = sticker[0];
        // 첫번쨰 스티커를 뜯지 않았을 경우
        dp2[0] = 0;
        dp2[1] = sticker[1];
        
        for (int i = 2; i < sticker.length; i++) {
            dp2[i] = Math.max(dp2[i-2]+sticker[i], dp2[i-1]);
            if (i < sticker.length-1) {
                dp1[i] = Math.max(dp1[i-2]+sticker[i], dp1[i-1]);
            }
        }
        
//         System.out.println(Arrays.toString(dp1));
//         System.out.println(Arrays.toString(dp2));
        int max1 = Arrays.stream(dp1).max().getAsInt();
        int max2 = Arrays.stream(dp2).max().getAsInt();
        return Math.max(max1, max2);
    }
}
```
좋아요를 가장 많이 받은 풀이이다.   
같은 풀이이다.   
```
public class Solution {
    public int solution(int[] sticker) {
        if(sticker.length == 1){
            return sticker[0];
        } else if(sticker.length == 2){
            return Math.max(sticker[0], sticker[1]);
        } else {
            return Math.max(findMaxSum(0, sticker.length - 2, sticker), findMaxSum(1, sticker.length - 1, sticker));
        }
    }

    private int findMaxSum(int from, int to, int[] sticker) {
        int[] sumArr = new int[sticker.length - 1];
        sumArr[0] = sticker[from];
        sumArr[1] = Math.max(sticker[from + 1], sticker[from]);
        for (int i = from + 2, sumIndex = 2; i <= to; i++, sumIndex++) {
            sumArr[sumIndex] = Math.max((sticker[i] + sumArr[sumIndex - 2]), sumArr[sumIndex - 1]);
        }
        return sumArr[sumArr.length - 1];
    }
}
```
