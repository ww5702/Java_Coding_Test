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
이처럼 섬을 연결하던가 할때 유니온-파인드가 가능한지 생각해보는것이 좋다.   
훨씬 빠르고 간편할 수 있다.   
```
import java.util.Arrays;
class Solution {
    static int[] parent;
    public static void union(int a, int b) {
    	a = find(a);
    	b = find(b);
    	if(a != b)
    		parent[b] = a;
    }
    
    public static int find(int x) {
	    if(parent[x] == x) return x;
	    return find(parent[x]);
    }   
    
    public int solution(int n, int[][] costs) {
        int answer = 0;
        parent = new int[n];
        for (int i = 0; i < parent.length; i++) parent[i] = i;
        Arrays.sort(costs, (o1,o2) -> {
            return o1[2] - o2[2];
        });
        //System.out.println(Arrays.toString(parent));
        //System.out.println(Arrays.deepToString(costs));
        
        for (int[] cost : costs) {
            int start = cost[0];
            int end = cost[1];
            int value = cost[2];
            if (find(start) != find(end)) {
                
                union(start, end);
                answer += value;
            }
            
        }
        
        return answer;
    }
}
```
좋아요를 가장 많이 받은 문제풀이 또한 유니온-파인드로 풀이하였다.   
