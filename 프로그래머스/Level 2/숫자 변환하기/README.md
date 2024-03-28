역으로 40에서 10으로 내려가면서 숫자를 찾는다.   
x = 10, y = 40, n = 5일때   
40-5 , 40/3 , 40/2 중 가장 큰 값에서부터 x까지 -하면서 순환한다.   
dp[i] = min(dp[i+n] + 1 , dp[i*3] + 1, dp[i*2] + 1)으로 점화식을 만든다.   
20일때 25에서 5를 뺀다 or 40에서 2를 나눈다 or 60에서 3을 나눈다 중 가장 작은 수로 바꾼다.   
y를 넘어가는 값은 전부 INF로 만들어 min에 걸리지 않도록 한다.   
```
import java.util.*;
class Solution {
    int[] dp = new int[3000003];
    int INF = 1000002;
    public int solution(int x, int y, int n) {
        int answer = 0;
        Arrays.fill(dp, INF);
        dp[x] = -1;
        dp[y] = 0;
        for(int num = Math.max(y - n, Math.max(y / 2, y / 3)); num >= x; num--){
            dp[num] = Math.min(dp[num + n] + 1, Math.min(dp[num * 2] + 1, dp[num * 3] + 1));
        }
        return dp[x] >= INF ? -1 : dp[x];
    }
}
```
