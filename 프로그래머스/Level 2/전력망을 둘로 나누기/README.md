```
import java.util.*;
class Solution {
    static int[][] graph;
    static boolean[] visited;
    static int N;
    public int solution(int n, int[][] wires) {
        graph = new int[n+1][n+1];
        visited = new boolean[n+1];
        N = n;
        int answer = n;
        for(int[] wire : wires) {
            graph[wire[0]][wire[1]] = 1;
            graph[wire[1]][wire[0]] = 1;
        }
        // for (int i = 1; i <= n; i++) {
        //     System.out.println(Arrays.toString(graph[i]));
        // }
        //System.out.println(Arrays.toString(visited));
        for (int[] wire: wires) {
            graph[wire[0]][wire[1]] = 0;
            graph[wire[1]][wire[0]] = 0;
            
            visited = new boolean[n+1];
            int cnt = bfs(1);
            //System.out.println(cnt+" "+(n-cnt));
            if (answer > (Math.abs((n-cnt) - cnt))) {
                answer = Math.abs((n-cnt) - cnt);
            }
            
            graph[wire[0]][wire[1]] = 1;
            graph[wire[1]][wire[0]] = 1;
        }
        
        
        return answer;
    }
    public int bfs(int start) {
        Queue<Integer> q = new LinkedList<>();
        q.add(start);
        visited[start] = true;
        int cnt = 1;
        //System.out.println(Arrays.toString(visited));
        while (!q.isEmpty()) {
            int now = q.poll();
            for (int i = 1; i <= N; i++) {
                if (!visited[i] && graph[now][i] == 1) {
                    visited[i] = true;
                    q.add(i);
                    cnt += 1;
                }
            }
        }
        return cnt;
    }
}
```
