출발지에서 레버까지   
레버에서 탈출구까지   
두번의 bfs를 돌린다.   
출발지에서 레버까지 못가면 return -1   
dis[] 초기화   
q 초기화   
레버에서 탈출구까지 못가면 return -1   
잘 도착했다면 return answer   

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
    static int[] dy = {-1,1,0,0};
    static int[] dx = {0,0,1,-1};
    public int solution(String[] maps) {
        int answer = 0;
        String[][] board = new String[maps.length][maps[0].length()];
        Integer[][] dis = new Integer[maps.length][maps[0].length()];
        Queue<Point> q = new LinkedList<>();
        int endY = 0;
        int endX = 0;
        int labberY = 0;
        int labberX = 0;
        
        for (int i = 0; i < maps.length; i++) {
            String[] input = maps[i].split("");
            for (int j = 0; j < input.length; j++) {
                board[i][j] = input[j];
                dis[i][j] = Integer.MAX_VALUE;
                if (board[i][j].equals("S")) {
                    q.add(new Point(i,j));
                    dis[i][j] = 0;
                } else if (board[i][j].equals("E")) {
                    endY = i;
                    endX = j;
                } else if (board[i][j].equals("L")) {
                    labberY = i;
                    labberX = j;
                }
            }
        }
        // for (int i = 0; i < maps.length; i++) {
        //     System.out.println(Arrays.toString(board[i]));
        // }
        
        while (!q.isEmpty()) {
            int ny = q.peek().y;
            int nx = q.peek().x;
            if (board[ny][nx].equals("L")) { 
                q.clear();
                q.add(new Point(ny,nx));
                break;
            }
            q.poll();
            
            for (int i = 0; i < 4; i++) {
                int newY = ny+dy[i];
                int newX = nx+dx[i];
                
                if (newY >= 0 && newY < board.length && newX >= 0 && newX < board[0].length) {
                    //System.out.println(newY+" "+newX);
                    if (!board[newY][newX].equals("X") && dis[newY][newX] > dis[ny][nx]+1) {
                        dis[newY][newX] = dis[ny][nx]+1;
                        q.add(new Point(newY,newX));
                    }
                }
            }
        }
        if (dis[labberY][labberX] == Integer.MAX_VALUE) {
            return -1;
        } else {
            answer += dis[labberY][labberX];
            //System.out.println(answer);
            for (int i = 0; i < dis.length; i++) {
                Arrays.fill(dis[i],Integer.MAX_VALUE);
            }
            dis[labberY][labberX] = 0;
        }
        // for (int i = 0; i < maps.length; i++) {
        //     System.out.println(Arrays.toString(dis[i]));
        // }
        
        while (!q.isEmpty()) {
            int ny = q.peek().y;
            int nx = q.peek().x;
            if (board[ny][nx].equals("E")) {
                answer += dis[ny][nx];
                break;
            }
            q.poll();
            
            for (int i = 0; i < 4; i++) {
                int newY = ny+dy[i];
                int newX = nx+dx[i];
                
                if (newY >= 0 && newY < board.length && newX >= 0 && newX < board[0].length) {
                    //System.out.println(newY+" "+newX);
                    if (!board[newY][newX].equals("X") && dis[newY][newX] > dis[ny][nx]+1) {
                        dis[newY][newX] = dis[ny][nx]+1;
                        q.add(new Point(newY,newX));
                    }
                }
            }
        }
        
        if (dis[endY][endX] == Integer.MAX_VALUE) {
            return -1;
        } else {
            return answer;
        }
    }
}
```
