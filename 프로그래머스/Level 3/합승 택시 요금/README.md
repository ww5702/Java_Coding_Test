n이 200밖게 안되기에 플로이드워셜 알고리즘으로 문제를 풀이할 수 있다.   
각 출발지에서 각 목표지점까지 최소 거리를 구해둔다.   
그리고 3중 반복문을 통해 i -> j까지 가는 거리를 i -> x + x -> a + x -> b   
이렇게 나눠서 구해준다.   

```
import java.util.Arrays;
import java.util.*;
class Solution {
    static int[][] fee;
    public int solution(int n, int s, int a, int b, int[][] fares) {
        
        int[][] fee = new int[n+1][n+1];
        for (int i = 1; i <= n; i++) {
            Arrays.fill(fee[i], 20000001);
            fee[i][i] = 0;
        }    
        
        for (int[] fare : fares) {
            fee[fare[0]][fare[1]] = fare[2];
            fee[fare[1]][fare[0]] = fare[2];
        }
        
        for (int k = 1; k <= n; k++) {
            for (int i = 1; i <= n; i++) {
                for (int j = 1; j <= n; j++) {
                    fee[i][j] = Math.min(fee[i][j], (fee[i][k] + fee[k][j]));
                }
            }
        }
        
//         for (int i = 1; i <= n; i++) {
//             System.out.println(Arrays.toString(fee[i]));
//         }
        int answer = fee[s][a] + fee[s][b];
        for (int i = 1; i <= n; i++) {
            answer = Math.min(answer, (fee[s][i] + fee[i][a] + fee[i][b]));
        }
        
        return answer;
    }
}
```
좋아요를 가장 많이 받은 풀이는 플로이드워셜이 아닌 다익스트라였다.   
java에는 pq가 있으므로 쉽게 풀이가 가능하다.   

```
import java.util.Arrays;
import java.util.*;
class Edge implements Comparable<Edge>{
    int index;
    int cost;
    Edge(int index, int cost){
        this.index = index;
        this.cost = cost;
    }
    @Override
    public int compareTo(Edge e){
        return this.cost - e.cost;
    }
}
class Solution {
    static final int MAX = 20000001; // 200 * 100000 + 1
    static ArrayList<ArrayList<Edge>> graph;
    
    static int[][] fee;
    public int solution(int n, int s, int a, int b, int[][] fares) {
        
        int answer = Integer.MAX_VALUE;

        graph = new ArrayList<>();
        for(int i = 0 ; i <= n ; i ++){
            graph.add(new ArrayList<>());
        }

        for(int[] i : fares){
            graph.get(i[0]).add(new Edge(i[1], i[2]));
            graph.get(i[1]).add(new Edge(i[0], i[2]));
        }
        
        int[] startA = new int[n + 1];
        int[] startB = new int[n + 1];
        int[] start = new int[n + 1];

        Arrays.fill(startA, MAX);
        Arrays.fill(startB, MAX);
        Arrays.fill(start, MAX);
        
        startA = dijkstra(a, startA);
        startB = dijkstra(b, startB);
        start = dijkstra(s, start);
        
        for (int i = 1; i <= n; i++) {
            answer = Math.min(answer, startA[i] + startB[i] + start[i]);
        }
        
        return answer;
    }
    static int[] dijkstra(int start, int[] costs) {
        PriorityQueue<Edge> pq = new PriorityQueue<>();
        pq.offer(new Edge(start, 0));
        costs[start] = 0;
        
        while (!pq.isEmpty()) {
            Edge now = pq.poll();
            int nidx = now.index;
            int ncost = now.cost;
            
            if (ncost > costs[nidx]) continue;
            
            ArrayList<Edge> edges = graph.get(nidx);
            for (Edge edge : edges) {
                int cost = costs[nidx] + edge.cost;
                
                if(cost < costs[edge.index]) {
                    costs[edge.index] = cost;
                    pq.offer(new Edge(edge.index, cost));
                }
            }
        }
        
        return costs;
    }
}
```
