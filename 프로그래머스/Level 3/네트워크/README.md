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
좋아요를 가장 많이 받은 풀이이다.   
푸는 방식은 dfs로 dfs bfs만 다르지 똑같았다.   
```
class Solution {
    public int solution(int n, int[][] computers) {
        int answer = 0;
        boolean[] chk = new boolean[n];
        for(int i = 0; i < n; i++) {
            if(!chk[i]) {
                dfs(computers, chk, i);
                answer++;
            }
        }
        return answer;
    }
    void dfs(int[][] computers, boolean[] chk, int start) {
        chk[start] = true;
        for(int i = 0; i < computers.length; i++) {
            if(computers[start][i] == 1 && !chk[i]) {
                dfs(computers, chk, i);
            }
        }
    }
}
```
