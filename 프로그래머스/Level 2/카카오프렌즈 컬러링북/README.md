bfs문제이다.   
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
    static boolean[][] visited;
    static int[] dy = {1,-1,0,0};
    static int[] dx = {0,0,1,-1};
    
    public int[] solution(int m, int n, int[][] picture) {
        visited = new boolean[m][n];
        int numberOfArea = 0;
        int maxSizeOfOneArea = 0;
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                //System.out.println(i+" "+j);
                if (!visited[i][j] && picture[i][j] != 0) {
                    numberOfArea += 1;
                    int cnt = bfs(picture,n,m,i,j,picture[i][j]);
                    maxSizeOfOneArea = Math.max(maxSizeOfOneArea, cnt);
                }
                
            }
        }
        
        int[] answer = new int[2];
        answer[0] = numberOfArea;
        answer[1] = maxSizeOfOneArea;
        return answer;
    }
    
    public int bfs(int[][] picture,int n, int m, int y, int x, int num) {
        Queue<Point> q = new LinkedList<>();
        q.add(new Point(y,x));
        int sum = 0;
        while (!q.isEmpty()) {
            int nowY = q.peek().y;
            int nowX = q.peek().x;
            //System.out.println("현재 "+nowY+" "+nowX);
            q.poll();
            for (int i = 0; i < 4; i++) {
                int newY = nowY + dy[i];
                int newX = nowX + dx[i];
                if (newY >= 0 && newY < m && newX >= 0 && newX < n) {
                    if (!visited[newY][newX] && picture[newY][newX] == num) {
                        //System.out.println(newY+" "+newX);
                        q.add(new Point(newY,newX));
                        visited[newY][newX] = true;
                        sum += 1;
                    }
                }
            }
        }
        return sum;
    }
}
```
