dfs로 풀이했으나 시간초과   

```
class Solution {
    public int[] result;
    int n;
    int answer;
    int solution(int[][] land) {
        answer = 0;
        n = land.length;
        dfs(-1, 0, land, 0);
        
        return answer;
    }
    
    public void dfs(Integer last, Integer depth, int[][] land, int result) {
        if (depth == n) {
            answer = Math.max(answer, result);
            return;
        }
        
        for (int i = 0; i < land[0].length; i++) {
            if (i == last) { continue; }
            dfs(i, depth+1, land, result + land[depth][i]);   
        }
    }
}
```
깊은 복사를 사용해야 한다.   
플로이드 워셜 알고리즘처럼 중간에 해당 위치를 들리면서   
물론 전에 밟았던 땅 j와 index값이 같다면 continue   
해당 땅을 밟았을때 더 크다면 값을 바꿔주는 형식으로 진행한다.   

```
import java.util.Arrays;
class Solution {
    int solution(int[][] land) {
        int[][] dp = new int[land.length][land[0].length];
        for (int i = 0; i < land.length; i++) {
            dp[i] = land[i].clone();
        }
        for (int i = 1; i < land.length; i++) {
            for (int j = 0; j < land[0].length; j++) {
                for (int k = 0; k < land[0].length; k++) {
                    if (j == k) { continue; }
                    dp[i][j] = Math.max(dp[i][j], dp[i-1][k] + land[i][j]);
                }
            }
        }
        return Arrays.stream(dp[land.length-1])
            .max()
            .getAsInt();
    }
    
}
```
