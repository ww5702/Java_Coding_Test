bfs 문제이다.   

```
import java.util.*;
import java.util.Arrays;
class Point {
    int y;
    int x;
    
    public Point(int y, int x) {
        this.y = y;
        this.x = x;
    }
}
class Solution {
    public int solution(String[] board) {
        int answer = 0;
        String[][] map = new String[board.length][board[0].length()];
        int startY = 0, startX = 0;
        int endY = 0, endX = 0;
        for (int i = 0; i < board.length; i++) {
            String[] now = board[i].split("");
            for (int j = 0; j < now.length; j++) {
                map[i][j] = now[j];
                if (map[i][j].equals("R")) {
                    startY = i;
                    startX = j;
                } else if (map[i][j].equals("G")) {
                    endY = i;
                    endX = j;
                }
            }
        }
        int[] dy = {1,-1,0,0};
        int[] dx = {0,0,1,-1};
        int[][] dis = new int[map.length][map[0].length];
        for (int i = 0; i < map.length; i++) {
            Arrays.fill(dis[i], 100001);
        }
        Queue<Point> q = new LinkedList<>();
        q.add(new Point(startY,startX));
        dis[startY][startX] = 0;
        
        while (!q.isEmpty()) {
            int nowY = q.peek().y;
            int nowX = q.peek().x;
            q.poll();
            for (int i = 0; i < 4; i++) {
                int tempY = nowY;
                int tempX = nowX;
                while (true) {
                    tempY += dy[i];
                    tempX += dx[i];
                    if (tempY >= 0 && tempY < map.length && tempX >= 0 && tempX < map[0].length) {
                        if (map[tempY][tempX].equals("D")) {
                            tempY -= dy[i];
                            tempX -= dx[i];
                            if (dis[tempY][tempX] > dis[nowY][nowX] + 1) {
                                dis[tempY][tempX] = dis[nowY][nowX] + 1;
                                q.add(new Point(tempY, tempX));
                            }
                            break;
                        } 
                    } else {
                        tempY -= dy[i];
                        tempX -= dx[i];
                        if (dis[tempY][tempX] > dis[nowY][nowX] + 1) {
                            dis[tempY][tempX] = dis[nowY][nowX] + 1;
                            q.add(new Point(tempY, tempX));
                        }
                        break;
                    }
                }
            }
        }
        // for (int i = 0; i < dis.length; i++) {
        //     System.out.println(Arrays.toString(dis[i]));
        // }
        // System.out.println(dis[endY][endX]);
        return dis[endY][endX] == 100001 ? -1 : dis[endY][endX];
    }
}
```
