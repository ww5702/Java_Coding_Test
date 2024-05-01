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
따라서 dfs한번만에 구할 수 있도록 풀이해봤지만 시간초과 발생   

```
import java.util.Arrays;
import java.util.*;
class Solution {
    static int[][] dis;
    static int[][] map;
    static int[] dy;
    static int[] dx;
    static int answer;
    static int num;
    public int solution(int m, int n, int[][] puddles) {
        answer = 0;
        map = new int[n][m];
        num = 100001;
        dy = new int[] {1,0};
        dx = new int[] {0,1};
        for (int[] puddle : puddles) {
            map[puddle[1]-1][puddle[0]-1] = 1;
        }
        //System.out.println(Arrays.deepToString(map));
        
        dfs(m,n,0,0,0);
        
        return answer % 1_000_000_007;
    }
    
    public void dfs(int m, int n, int y, int x, int cnt) {
        // 어차피 최단거리만
        if (cnt > num) { return; }
        
        if (y == n-1 && x == m-1) {
            //System.out.println("도착");
            if (cnt < num) {
                //System.out.println("갱신 "+cnt);
                num = cnt;
                answer = 1;
            } else if (cnt == num) {
                //System.out.println("같다");
                answer += 1;
            }
        }
        
        for (int i = 0; i < 2; i++) {
            int newY = y + dy[i];
            int newX = x + dx[i];
            if (newY >= 0 && newY < n && newX >= 0 && newX < m) {
                if (map[newY][newX] != 1) {
                    //System.out.println(newY+" "+newX);
                    dfs(m,n,newY,newX,cnt+1);
                }
            }
            
        }
        
    }
}
```
따라서 누적합 개념으로 해당 좌표를 윗쪽과 왼쪽에서 올수있다면   
윗쪽에서 오는 경우 + 왼쪽에서 오는 경우를 합해서 넣어줬다.   

```
import java.util.Arrays;
import java.util.*;
class Solution {
    public int solution(int m, int n, int[][] puddles) {
        int mod = 1000000007;
        int[][] map = new int[n+1][m+1];
        int[] dy = new int[] {1,0};
        int[] dx = new int[] {0,1};
        for (int[] puddle : puddles) {
            map[puddle[1]][puddle[0]] = -1;
        }
        map[1][1] = 1;
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                if (map[i][j] == -1) continue;
                if (map[i-1][j] > 0) map[i][j] += map[i-1][j] % mod;
                if (map[i][j-1] > 0) map[i][j] += map[i][j-1] % mod;
            }
        }
        //System.out.println(Arrays.deepToString(map));
        
        return map[n][m] % mod;
    }
}
```
좋아요를 가장 많이 받은 풀이도 위와 같았다.   
