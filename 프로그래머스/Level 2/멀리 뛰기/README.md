피보나치는 실패   
```
import java.util.*;
import java.util.Arrays;
class Solution {
    HashMap<Integer, Integer> dict = new HashMap<>();
    
    public long jump(int n) {
        if (dict.get(n) != null) {
            return dict.get(n);
        }
        
        return ((jump(n-1) + jump(n-2)) % 1234567);
    }
    
    public long solution(int n) {
        dict.put(0, 0);
        dict.put(1, 1);
        dict.put(2, 2);
        
        return jump(n);
    }
    
    
}
```
따라서 동적게획법으로 풀이   
n으로 가는 정답은 n-1에서 1 올라가거나 / n-2에서 2올라가는 경우이다.   
```
class Solution {
    long[] dp = new long[2001];
    public long solution(int n) {
        dp[0] = 0;
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i < dp.length; i++) {
            dp[i] = (dp[i - 1] + dp[i - 2]) % 1234567;
        }
        return dp[n];
  }
}
```
