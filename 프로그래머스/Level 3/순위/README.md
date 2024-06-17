dfs로 순환하면서 내가 이미 이긴 녀석이 이긴사람도 내가 이기는 구조로 저장한다.   
만약 내가 이긴 사람 + 내가 진 사람이 n-1이라면 순위를 정확하게 알 수 있다.   

```
import java.util.*;
class Solution {
    static boolean[] visited;
    static int[] strongCnt;
    static int[] weakCnt;
    static int cnt;
    public int solution(int n, int[][] results) {
        int answer = 0;
        strongCnt = new int[n+1];
        weakCnt = new int[n+1];
        ArrayList<Integer>[] list = new ArrayList[n+1];
        for (int i = 0; i <= n; i++) {
            list[i] = new ArrayList<>();
        }
        for (int[] result: results) {
            list[result[0]].add(result[1]);
        }
        visited = new boolean[n+1];
        
        for (int i = 1; i <= n; i++) {
            visited = new boolean[n+1];
            cnt = 0;
            dfs(list, i);
            //System.out.println(cnt);
            strongCnt[i] = cnt;
            //System.out.println(Arrays.toString(strongCnt));
            //System.out.println(Arrays.toString(weakCnt));
        }
        
        for (int i = 1; i <= n; i++) {
            answer += (strongCnt[i] + weakCnt[i] == n-1) ? 1 : 0;
        }
        
        return answer;
    }
    public int dfs(ArrayList<Integer>[] list, int n) {
        //System.out.println(list[n].toString());
        visited[n] = true;
        
        for (int next : list[n]) {
            if (!visited[next]) {
                weakCnt[next] += 1;
                cnt += 1;
                dfs(list, next);
            }
        }
        return cnt;
    }
    
    
}
```
