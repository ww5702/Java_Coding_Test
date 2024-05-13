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
틀린 이유는 과정에서 해당 좌표에서 적은 코스트로 지나갔는데   
결과론적으로 해당 좌표로 지나갔을때 더 적은값으로 결과값에 도달할때가 존재하기에   
틀리는 테케들이 있는 것이다.   
따라서 dfs로 전부 실행 후 정답좌표의 값들을 비교해보았다.   
```
import java.util.*;
import java.util.Arrays;
class Solution {
    static int[] dy;
    static int[] dx;
    static boolean[][] visited;
    static int answer;
    public int solution(int[][] board) {
        dy = new int[] {1,-1,0,0};
        dx = new int[] {0,0,1,-1};
        visited = new boolean[board.length][board[0].length];
        visited[0][0] = true;
        
        answer = Integer.MAX_VALUE;
        dfs(board,0,0,-1,0);
        
        return answer;
    }
    
    public void dfs(int[][] board, int y, int x, int dir, int cost) {
        if (y == board.length-1 && x == board[0].length-1) {
            answer = Math.min(answer, cost);
            return;
        }
        
        for (int i = 0; i < 4; i++) {
            int newY = y + dy[i];
            int newX = x + dx[i];
            if (newY >= 0 && newY < board.length && newX >= 0 && newX < board[0].length) {
                // 벽이 아니고
                if (board[newY][newX] != 1) {
                    // 첫번째 움직임인지
                    if (!visited[newY][newX]) {
                        if (i == dir || dir == -1) {
                            visited[newY][newX] = true;
                            dfs(board,newY,newX,i,cost+100);
                            visited[newY][newX] = false;
                        } else {
                            visited[newY][newX] = true;
                            dfs(board,newY,newX,i,cost+600);
                            visited[newY][newX] = false;
                        }
                    }
                    
                }
            }
        }
        return;
    }
}
```
하지만 해당 경우는 시간초과가 발생한다.   
따라서 dp밖에 남지 않아 동적계획법으로 구현해보았다.   
```

```
