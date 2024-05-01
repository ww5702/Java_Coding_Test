최단거리를 찾는 bfs를 한번, 경로를 찾는 dfs를 한번 실행했다.   
하지만 효율성 테스트에서 시간초과가 발생하였다.   

```
import java.util.Arrays;
import java.util.*;
class Point {
    int y;
    int x;
    public Point(int y, int x) {
        this.y = y;
        this.x = x;
    }
}
class Solution {
    static int[][] dis;
    static int[][] map;
    static int[] dy;
    static int[] dx;
    static int answer;
    public int solution(int m, int n, int[][] puddles) {
        answer = 0;
        map = new int[n][m];
        dy = new int[] {1,0};
        dx = new int[] {0,1};
        for (int[] puddle : puddles) {
            map[puddle[1]-1][puddle[0]-1] = 1;
        }
        //System.out.println(Arrays.deepToString(map));
        dis = new int[n][m];
        for (int i = 0; i < n; i++) {
            Arrays.fill(dis[i], 100001);
        }
        dis[0][0] = 0;
        
        bfs(m,n,0,0);
        int num = dis[n-1][m-1];
        dfs(m,n,0,0,num,0);
        // for (int i = 0; i < n; i++) {
        //     System.out.println(Arrays.toString(dis[i]));
        // }
        
        return answer % 1_000_000_007;
    }
    
    public void bfs(int m, int n, int y, int x) {
        Queue<Point> q = new LinkedList<>();
        q.add(new Point(y,x));
        
        while (!q.isEmpty()) {
            int nowY = q.peek().y;
            int nowX = q.peek().x;
            q.poll();
            for (int i = 0; i < 2; i++) {
                int newY = nowY + dy[i];
                int newX = nowX + dx[i];
                if (newY >= 0 && newY < n && newX >= 0 && newX < m) {
                    if (map[newY][newX] != 1 && dis[newY][newX] > dis[nowY][nowX] + 1) {
                        q.add(new Point(newY,newX));
                        dis[newY][newX] = dis[nowY][nowX] + 1;
                    }  
                }
            }
        }
    }
    
    public void dfs(int m, int n, int y, int x, int num, int cnt) {
        if (cnt == num && y == n-1 && x == m-1) {
            answer += 1;
            return;
        } 
        
        for (int i = 0; i < 2; i++) {
            int newY = y + dy[i];
            int newX = x + dx[i];
            if (newY >= 0 && newY < n && newX >= 0 && newX < m) {
                if (map[newY][newX] != 1) {
                    dfs(m,n,newY,newX,num,cnt+1);
                }
            }
            
        }
        
    }
}
```
