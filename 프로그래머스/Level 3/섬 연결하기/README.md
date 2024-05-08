그래프를 만들어 최단거리를 구하는줄 알았으나   
0으로 예를 들었을떄 0에서 출발하는 2까지의 거리는 2이지만   
1에서 출발하는 2까지의 거리는 1이다.   

```
import java.util.*;
import java.util.Arrays;
class Point {
    int arrive;
    int cost;
    
    public Point(int arrive, int cost) {
        this.arrive = arrive;
        this.cost = cost;
    }
}
class Solution {
    public int solution(int n, int[][] costs) {
        int answer = 0;
        ArrayList<Point>[] list = new ArrayList[n];
        for (int i = 0; i < n; i++) {
            list[i] = new ArrayList<>();
        }
        for (int[] cost: costs) {
            list[cost[0]].add(new Point(cost[1],cost[2]));
            list[cost[1]].add(new Point(cost[0],cost[2]));
        }
        
        for (int i = 0; i < n; i++) {
            System.out.println(list[i].toString());
        }
        
        int[] dis = new int[n];
        Arrays.fill(dis, Integer.MAX_VALUE);
        dis[costs[0][0]] = 0;
        
        // bfs
        Queue<Point> q = new LinkedList<>();
        q.add(new Point(costs[0][0], 0));
        
        while (!q.isEmpty()) {
            Point now = q.poll();
            System.out.println(now.arrive+" "+now.cost);
            for (Point next : list[now.arrive]) {
                System.out.println(next.arrive+" "+next.cost);
                if (dis[next.arrive] > dis[now.arrive] + next.cost) {
                    dis[next.arrive] = dis[now.arrive] + next.cost;
                    q.add(new Point(next.arrive, dis[next.arrive]));
                    
                }
            }
            System.out.println(Arrays.toString(dis));
        }
        
        
        return answer;
    }
}
```
