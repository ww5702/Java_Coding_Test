단순 bfs문제이지만, 효율성 문제때문에 좀더 생각을 해서 풀이해보았다.   
list를 이용해 해당 좌표로 연결되는 석유의 갯수들을 지정해두었다.   
```
import java.util.*;
import java.util.Arrays;
class Point {
    int y;
    int x;
    public Point (int y, int x) {
        this.y = y;
        this.x = x;
    }
}
class Solution {
    static boolean[][] visited;
    static int[][] map;
    static int[] dy = {1,-1,0,0};
    static int[] dx = {0,0,1,-1};
    public int solution(int[][] land) {
        int answer = 0;
        map = new int[land.length][land[0].length];
        List<Integer> list = new ArrayList<>();
        list.add(0);
        visited = new boolean[land.length][land[0].length];
        int num = 1;
        for (int i = 0; i < land.length; i++) {
            for (int j = 0; j < land[0].length; j++) {
                if (!visited[i][j] && land[i][j] == 1) {
                    list.add(bfs(land,i,j,num++));
                }
            }
        }
        // for (int i = 0; i < land.length; i++) {
        //     System.out.println(Arrays.toString(map[i]));
        // }
        // System.out.println(list.toString());
        
        
        for (int j = 0; j < land[0].length; j++) {
            boolean[] newVisited = new boolean[num+1];
            int temp = 0;
            for (int i = 0; i < land.length; i++) {
                if (!newVisited[map[i][j]]) {
                    temp += list.get(map[i][j]);
                    newVisited[map[i][j]] = true;
                }
            }
            answer = Math.max(answer,temp);
        }
        return answer;
    }
    
    public int bfs(int[][] land, int y, int x, int num) {
        Queue<Point> q = new LinkedList<>();
        q.add(new Point(y,x));
        visited[y][x] = true;
        map[y][x] = num;
        int sum = 1;
        while (!q.isEmpty()) {
            int nowY = q.peek().y;
            int nowX = q.peek().x;
            q.poll();
            
            for (int i = 0; i < 4; i++) {
                int newY = nowY + dy[i];
                int newX = nowX + dx[i];
                if (newY >= 0 && newY < land.length && 
                    newX >= 0 && newX < land[0].length) {
                    if (!visited[newY][newX] && land[newY][newX] == 1) {
                        q.add(new Point(newY,newX));
                        visited[newY][newX] = true;
                        map[newY][newX] = num;
                        sum += 1;
                    }
                }
            }
        }
        
        return sum;
    }
}[PCCP 기출문제] 2번 / 석유 시추
```
