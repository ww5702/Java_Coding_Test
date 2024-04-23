long으로 변환값을 바꿔준뒤 풀이해준다.   
dp[i]를 구할때 + mod를 해주는 이유는   
mod를 99라고 했을때   
원래 100 - 10 이었던 값이 1 - 10 이 되어 음수가 될수도 있다.   
```
import java.util.Arrays;
class Solution {
    public long solution(int n) {
        /*
        0 -> 1
        2 -> 3
        4 -> 11
        6 -> 51
        f(n) = f(n-2)*4 - f(n-4)
        */
        long[] dp = new long[n+1];
        long mod = 1_000_000_007;
        dp[0] = 1;
        dp[2] = 3;
        if (n >= 4) {
            for (int i = 4; i <= n; i += 2) {
                dp[i] = (dp[i-2]*4 - dp[i-4] + mod) % mod; 
            }
        }
        //System.out.println(Arrays.toString(dp));
        return dp[n];
    }
}
```
