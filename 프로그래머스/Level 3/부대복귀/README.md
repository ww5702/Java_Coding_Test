전형적인 연결리스트를 이용하녀 bfs로 최단거리 찾기 문제   

```
import java.util.*;
import java.util.Arrays;
class Solution {
    static ArrayList<Integer>[] list;
    static int[] dis;
    public int[] solution(int n, int[][] roads, int[] sources, int destination) {
        int[] answer = new int[sources.length];
        
        dis = new int[n+1];
        Arrays.fill(dis, Integer.MAX_VALUE);
        
        list = new ArrayList[n+1];
        for (int i = 0; i <= n; i++) {
            list[i] = new ArrayList<>();
        }
        for (int[] road : roads) {
            list[road[0]].add(road[1]);
            list[road[1]].add(road[0]);
        }
        bfs(destination);
        for (int i = 0; i < sources.length; i++) {
            answer[i] = dis[sources[i]] == Integer.MAX_VALUE ? -1 : dis[sources[i]];
        }
        
        return answer;
    }
    
    public void bfs(int node) {
        Queue<Integer> q = new LinkedList<>();
        q.add(node);
        dis[node] = 0;
        while (!q.isEmpty()) {
            int now = q.poll();
            
            for (int next : list[now]) {
                if (dis[next] > dis[now]+1) {
                    q.add(next);
                    dis[next] = dis[now]+1;
                }
            }
        }
    }
}
```
