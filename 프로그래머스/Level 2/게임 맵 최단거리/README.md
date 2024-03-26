```
import java.util.*;
import java.util.Arrays;
class Point {
    public int y,x;
    Point(int y, int x) {
        this.y = y;
        this.x = x;
    }
}
class Solution {
    static int n;
    static int m;
    static int[] dy = {1,-1,0,0};
    static int[] dx = {0,0,1,-1};
    static int[][] result;
    
    public int solution(int[][] maps) {
        int answer = 0;
        n = maps.length;
        m = maps[0].length;
        result = new int[n][m];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                result[i][j] = Integer.MAX_VALUE;
            }
        }
        
        //System.out.println(Arrays.deepToString(maps));
        bfs(maps,0,0);
        //System.out.println(Arrays.deepToString(result));
        answer = result[n-1][m-1];
        return answer == Integer.MAX_VALUE ? -1 : answer;
    }
    public void bfs(int[][] maps, int y, int x) {
        Queue<Point> q = new LinkedList<>();
        q.offer(new Point(y,x));
        result[y][x] = 1;
        while (!q.isEmpty()) {
            Point now = q.poll();
            for (int i = 0; i < 4; i++) {
                int ny = now.y + dy[i];
                int nx = now.x + dx[i];
                if (ny >= 0 && ny < n && nx >= 0 && nx < m && maps[ny][nx] != 0) {
                    if (result[ny][nx] > result[now.y][now.x]+1) {
                        result[ny][nx] = result[now.y][now.x] + 1;
                        q.offer(new Point(ny,nx));
                    }
                }
            }
        }
    }
}
```
