list안에 point로 만든 배열을 넣는다.   
해당 리스트 안에 경로를 넣어준다.   
q에 1을 넣어주고,   
dis를 INT.MAX로 초기화해준다.   
더 짧은 경로가 발견되면 q에 넣어주고, 반복문을 수행한다.   
```
import java.util.*;
import java.util.Arrays;
class Point {
    int end;
    int cost;
    
    public Point(int end, int cost) {
        this.end = end;
        this.cost = cost;
    }
}
class Solution {
    static List<Point> list;
    public long solution(int N, int[][] road, int K) {
        int answer = 0;
        ArrayList<Point>[] list = new ArrayList[N+1];
        int[] dis = new int[N+1];
        Queue<Point> q = new LinkedList<>();
        //초기화
        for(int i=1;i<N+1;i++){
            list[i] = new ArrayList<>();
            dis[i] = Integer.MAX_VALUE;
        }
        dis[1] = 0;
        
        for (int i = 0; i < road.length; i++) {
            int[] value = road[i];
            int start = value[0];
            int end = value[1];
            int cost = value[2];
            list[start].add(new Point(end,cost));
            list[end].add(new Point(start,cost));
        }
        
        q.add(new Point(1,0));
        
        while (!q.isEmpty()) {
            int now = q.peek().end;
            int cost = q.peek().cost;
            q.poll();
            
            for (int i = 0; i < list[now].size(); i++) {
                //System.out.println(list[now].get(i).end);
                int newEnd = list[now].get(i).end;
                int newCost = list[now].get(i).cost;
                if (dis[newEnd] > dis[now] + newCost) {
                    dis[newEnd] = dis[now] + newCost;
                    q.add(new Point(newEnd, dis[newEnd]));
                }
            }
        }
        return Arrays.stream(dis).filter(i -> i <= K).count()-1;
    }
}
```
