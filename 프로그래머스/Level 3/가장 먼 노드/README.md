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
좋아요를 가장 많이 받은 풀이 또한 나와 같은 풀이로 풀이하였다.   
하지만 연결리스트를 구현하는 부분이 조금 달랐고,   
bfs를 진행하면서 어차피 이동한다면 최단거리로 이동이 가능하다   
따라서 그냥 변경해주어도 가능하다는 것을 알았다.   
```
import java.util.ArrayList;

class Solution {
    public int solution(int n, int[][] edge) {
        ArrayList<Integer>[] path = new ArrayList[n];
        ArrayList<Integer> bfs = new ArrayList<Integer>();
        int answer = 0;
        int[] dist = new int[n];
        dist[0] = 1;
        int max = 0;

        for(int i = 0; i < edge.length; i++) {
            int num1 = edge[i][0] - 1;
            int num2 = edge[i][1] - 1;
            if(path[num1] == null)
                path[num1] = new ArrayList<Integer>();
            if(path[num2] == null)
                path[num2] = new ArrayList<Integer>();
            path[num1].add(num2);
            path[num2].add(num1);
        }

        bfs.add(0);
        while(!bfs.isEmpty()) {
            int idx = bfs.get(0);
            bfs.remove(0);
            while(!path[idx].isEmpty()) {
                int num = path[idx].get(0);
                path[idx].remove(0);
                bfs.add(num);
                if(dist[num] == 0) {
                    dist[num] = dist[idx] + 1;
                    max = dist[num];
                }
            }
        }
        for(int i = 0; i < n; i++) {
            if(dist[i] == max)
                answer++;
        }

        return answer;
    }
}
```
따라서 맨 처음 코드를 이렇게 바꿀 수 있었다.   

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
        Queue<Integer> q = new LinkedList<>();
        q.add(1);
        dis[0] = 1;
        int maxCnt = 0;
        
        while (!q.isEmpty()) {
            int now = q.poll();
            
            for (int next : list[now]) {
                if (dis[next-1] == 0) {
                    dis[next-1] = dis[now-1] + 1;
                    q.add(next);
                    maxCnt = dis[next-1];
                }
            }
        }
        
        //System.out.println(Arrays.toString(dis));
        int cnt = maxCnt;
        return Arrays.stream(dis).filter(i -> i == cnt).count();
    }
}
```
