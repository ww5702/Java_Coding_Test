간선을 연결해주고, 1에서 출발하여 최단거리를 bfs로 구해준다.   
구한 거리 배열에서 최대값을 maxCnt로 구하고,   
maxCnt와 같은값을 return해준다.   
```
import java.util.Arrays;
import java.util.*;
class Solution {
    public long solution(int n, int[][] edge) {
        ArrayList<Integer>[] list = new ArrayList[n+1];
        for (int i = 0; i <= n; i++) {
            list[i] = new ArrayList<>();
        }
        for (int[] e : edge) {
            list[e[0]].add(e[1]);
            list[e[1]].add(e[0]);
        }
        
        // for (int i = 1; i <= n; i++) {
        //     System.out.println(list[i].toString());
        // }
        
        int[] dis = new int[n];
        Arrays.fill(dis, Integer.MAX_VALUE);
        dis[0] = 0;
        Queue<Integer> q = new LinkedList<>();
        q.add(1);
        
        while (!q.isEmpty()) {
            int now = q.poll();
            
            for (int next : list[now]) {
                if (dis[next-1] > dis[now-1] + 1) {
                    dis[next-1] = dis[now-1] + 1;
                    q.add(next);
                }
            }
        }
        
        //System.out.println(Arrays.toString(dis));
        int maxCnt = Arrays.stream(dis).max().getAsInt();
        return Arrays.stream(dis).filter(i -> i == maxCnt).count();
    }
}
```
