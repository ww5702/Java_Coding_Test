노드들이 도착하지 못하는 노드이자 연결하는 간선도 없다면 정점노드이다.   
순환방식은 이와 같게 했다.   
bfs(루트에서 연결된 노드) {    
노드의 진출차수가 2개인 노드가 있다 -> 8자모양(3)   
시작 노드로 돌아왔다 -> 도넛모양(1)   
사이클이 발생하지 않는다 -> 막대모양(2)   
}   
하지만 실패하는 테케들이 꽤 있었다.   
``` 
import java.util.Arrays;
import java.util.*;
class Solution {
    static int n;
    static boolean[] visited;
    public int[] solution(int[][] edges) {
        int[] answer = new int[4];
        int start = 0;
        n = Arrays.stream(edges).flatMapToInt(Arrays::stream).max().orElseThrow();
        visited = new boolean[n+1];
        ArrayList<Integer>[] list = new ArrayList[n+1];
        for (int i = 0; i <= n; i++) {
            list[i] = new ArrayList<>();
        }
        for (int[] edge : edges) {
            list[edge[0]].add(edge[1]);
            visited[edge[1]] = true;
        }
        // for (int i = 0; i <= n; i++) {
        //     System.out.println(list[i].toString());
        // }
        //System.out.println(Arrays.toString(visited));
        for (int i = 1; i <= n; i++) {
            if (!visited[i] && list[i].size() != 0) {
                start = i;
                answer[0] = start;
                break;
            }
        }
        //System.out.println("start = "+start);
        for (int next : list[start]) {
            //System.out.println(next);
            String value = bfs(list,next);
            if (value.equals("donut")) {
                answer[1] += 1;
            } else if (value.equals("stick")) {
                answer[2] += 1;
            } else if (value.equals("eight")) {
                answer[3] += 1;
            }
        }
        return answer;
    }
    public String bfs(ArrayList<Integer>[] list, int now) {
        visited = new boolean[n+1];
        visited[now] = true;
        Queue<Integer> q = new LinkedList<>();
        q.add(now);
        
        while(!q.isEmpty()) {
            int cur = q.poll();
            if (list[cur].size() == 2) {
                return "eight";
            }
            for (int c : list[cur]) {
                if (c == now) {
                    return "donut";
                }
                q.add(c);
            }
        }
        return "stick";
    }
    
}
```
