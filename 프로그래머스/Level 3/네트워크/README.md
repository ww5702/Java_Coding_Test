전형적인 사이클 탐색 문제이다.   

```
import java.util.*;
class Solution {
    static boolean[] visited;
    public int solution(int n, int[][] computers) {
        int answer = 0;
        visited = new boolean[computers.length];
        
        for (int i = 0; i < computers.length; i++) {
            //System.out.println(Arrays.toString(visited));
            if (!visited[i]) {
                visited[i] = true;
                answer += 1;
                bfs(computers, i);
            }
        }
        
        return answer;
    }
    public void bfs(int[][] computers, int node) {
        Queue<Integer> q = new LinkedList<>();
        q.add(node);
        while (!q.isEmpty()) {
            int now = q.poll();
            for (int i = 0; i < computers[now].length; i++) {
                if (computers[now][i] == 1 && !visited[i]) {
                    visited[i] = true;
                    q.add(i);
                }
            }
        }
        
    }
}
```
