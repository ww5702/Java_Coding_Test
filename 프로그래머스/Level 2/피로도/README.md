dfs를 이용하여 풀이하는 문제   
```
import java.util.Arrays;
class Solution {
    public static boolean visited[];
    public static int answer;
    public int solution(int k, int[][] dungeons) {
        answer = -1;
        visited = new boolean[dungeons.length];
        dfs(k, dungeons, 0);
        return answer;
    }
    public static void dfs(int tired, int[][] dungeons, int cnt){
        for (int i = 0; i < dungeons.length; i++) {
            if (!visited[i] && tired >= dungeons[i][0]) {
                visited[i] = true;
                dfs(tired - dungeons[i][1], dungeons, cnt+1);
                visited[i] = false;
            }
        }
        answer = Math.max(answer, cnt);
        
    }
}
```
