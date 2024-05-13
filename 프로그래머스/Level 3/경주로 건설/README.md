bfs로 풀이하되 방향이 같으면 100, 다르면 꺾고 직진인 600으로 계산하여   
비용이 적어진다면 추가로 진행하였다.   
또한 비용이 같더라도, 방향에 따른 변수가 존재하기 때문에 비용이 같더라도   
추가하도록 진행해보았다.   
```
import java.util.*;
import java.util.Arrays;
class Point {
    int y;
    int x;
    int dir;
    int cost;
    public Point(int y, int x, int dir, int cost) {
        this.y = y;
        this.x = x;
        this.dir = dir;
        this.cost = cost;
    }
}
class Solution {
    static int[] dy;
    static int[] dx;
    static int[][] result;
    public int solution(int[][] board) {
        dy = new int[] {1,-1,0,0};
        dx = new int[] {0,0,1,-1};
        result = new int[board.length][board[0].length];
        for (int i = 0; i < board.length; i++) {
            Arrays.fill(result[i], Integer.MAX_VALUE);
        }
        result[0][0] = 0;
        bfs(board,0,0);
        // for (int i = 0; i < board.length; i++) {
        //    System.out.println(Arrays.toString(result[i]));
        // }
        int answer = 0;
        return result[board.length-1][board[0].length-1];
    }
    
    public void bfs(int[][] board, int y, int x) {
        Queue<Point> q = new LinkedList<>();
        q.add(new Point(y,x,-1,0));
        
        while (!q.isEmpty()) {
            Point now = q.poll();
            int ny = now.y;
            int nx = now.x;
            int dir = now.dir;
            int cost = now.cost;
            
            for (int i = 0; i < 4; i++) {
                int newY = ny + dy[i];
                int newX = nx + dx[i];
                if (newY >= 0 && newY < board.length && newX >= 0 && newX < board[0].length) {
                    // 벽이 아니고
                    if (board[newY][newX] != 1) {
                        // 첫번째 움직임인지
                        if (dir == -1) {
                            result[newY][newX] = 100;
                            q.add(new Point(newY,newX,i,100));
                        } else {
                            if (i == dir) {
                                if (result[newY][newX] >= result[ny][nx] + 100) {
                                    //ystem.out.println(ny+" "+nx+" 같은 방향 "+newY+" "+newX);
                                    result[newY][newX] = result[ny][nx] + 100;
                                    q.add(new Point(newY,newX,i,result[newY][newX]));
                                }
                            } else {
                                if (result[newY][newX] >= result[ny][nx] + 600) {
                                    //System.out.println(ny+" "+nx+" 다른 방향 "+newY+" "+newX);
                                    result[newY][newX] = result[ny][nx] + 600;
                                    q.add(new Point(newY,newX,i,result[newY][newX]));
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
```
