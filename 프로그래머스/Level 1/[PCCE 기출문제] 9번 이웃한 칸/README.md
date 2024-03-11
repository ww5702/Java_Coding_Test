bfs의 기초이다.   
```
import java.util.Arrays;
class Solution {
    public int solution(String[][] board, int h, int w) {
        int answer = 0;
        String color = board[h][w];
        int dy[] = {-1,1,0,0};
        int dx[] = {0,0,-1,1};
        
        //System.out.println(color);
        for (int i = 0; i < 4; i++) {
            int curY = h + dy[i];
            int curX = w + dx[i];
            if (curY >= 0 && curY < board.length && curX >= 0 && curX < board.length) {
                //System.out.println(board[curY][curX]);
                answer += color.equals(board[curY][curX]) ? 1 : 0;
            }
        }
        
        return answer;
    }
}
```
