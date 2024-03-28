dfs로 풀이하였지만 시간초과 발생   
```
class Solution {
    static int answer;
    public int solution(int n) {
        answer = 0;
        dfs(0,n);
        return answer;
    }
    public void dfs(int depth, int target) {
        if (depth == target) {
            answer += 1;
            return;
        }
        
        if (depth <= target-2) {
            dfs(depth+2, target);
            dfs(depth+1, target);
        } else {
            dfs(depth+1, target);
        }
    }
}
```
어이없지만 등차수열로 수학문제였다   
1 2 3 5 8 13 등으로 무한히 증가하는 수열이다.   
```
class Solution {
    public int solution(int n) {
        int answer = 0;
        int[] dp = new int[n+1];
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i <= n; i++) {
            dp[i] = (dp[i-1]+dp[i-2]) % 1000000007;
        }
        return dp[n];
    }
}
```
