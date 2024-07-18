bfs로 각 알파벳으로 향하는 최단거리를 구하는 문제인것같았다.   
하지만 45점   

```
import java.util.*;
import java.io.*;
class Point {
    int y;
    int x;
    public Point(int y, int x) {
        this.y = y;
        this.x = x;
    }
}
class Main {
    static int n;
    static int[][] board;
    static int[][] strBoard;
    static int[][] dis;
    static int[] dy;
    static int[] dx;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        board = new int[n][n];
        strBoard = new int[5][2];
        dis = new int[n][n];
        dy = new int[] {1,-1,0,0};
        dx = new int[] {0,0,1,-1};
        for (int i = 0; i < n; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine(), " ");
            for (int j = 0; j < n; j++) {
                board[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        for (int i = 0; i < 5; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine(), " ");
            int y = Integer.parseInt(st.nextToken());
            int x = Integer.parseInt(st.nextToken());
            strBoard[i][0] = y-1;
            strBoard[i][1] = x-1;
        }


        int case1 = 0;
        int case2 = 0;

        // 첫번째 e를 밟을때
        int curY = 0;
        int curX = 0;
        for (int i = 0; i < 5; i++) {
            int goalY = strBoard[i][0];
            int goalX = strBoard[i][1];

            for (int j = 0; j < n; j++) {
                Arrays.fill(dis[j], 1000001);
            }
            //System.out.println(Arrays.deepToString(dis));
            int cost = bfs(curY,curX,goalY,goalX);
            // for (int k = 0; k < n; k++) {
            //     System.out.println(Arrays.toString(dis[k]));
            // }
            // System.out.println(case1+" "+cost);

            case1 += cost;
            curY = goalY;
            curX = goalX;
        }

        // 첫번째 e랑 두번째 e 스위치
        int tempY = strBoard[0][0];
        int tempX = strBoard[0][1];
        strBoard[0][0] = strBoard[4][0];
        strBoard[0][1] = strBoard[4][1];
        strBoard[4][0] = tempY;
        strBoard[4][1] = tempX;

        curY = 0;
        curX = 0;
        for (int i = 0; i < 5; i++) {
            int goalY = strBoard[i][0];
            int goalX = strBoard[i][1];

            for (int j = 0; j < n; j++) {
                Arrays.fill(dis[j], 1000001);
            }
            //System.out.println(Arrays.deepToString(dis));
            int cost = bfs(curY,curX,goalY,goalX);
            // for (int k = 0; k < n; k++) {
            //     System.out.println(Arrays.toString(dis[k]));
            // }
            //System.out.println(case2+" "+cost);

            case2 += cost;
            curY = goalY;
            curX = goalX;
        }
        System.out.println(case1 <= case2 ? case1 : case2);
    }

    /*
    각자의 단어로 이동하는 최단거리를 구한다
    */
    public static int bfs (int y, int x, int goalY, int goalX ) {
        Queue<Point> q = new LinkedList<>();
        q.add(new Point(y,x));
        dis[y][x] = 0;
        while (!q.isEmpty()) {
            Point now = q.poll();
            int nowY = now.y;
            int nowX = now.x;
            
            if (nowY == goalY && nowX == goalX) {
                return dis[goalY][goalX];
            }

            for (int i = 0; i < 4; i++) {
                int newY = nowY+dy[i];
                int newX = nowX+dx[i];
                if (newY >= 0 && newY < n && newX >= 0 && newX < n) {
                    if (dis[newY][newX] > dis[nowY][nowX] + board[newY][newX] + board[nowY][nowX]) {
                        q.add(new Point(newY,newX));
                        dis[newY][newX] = dis[nowY][nowX] + board[newY][newX] + board[nowY][nowX];
                    }
                }
            }
        }

        return -1;
    }
}
```
