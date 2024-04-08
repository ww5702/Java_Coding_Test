덮이는 숫자를 temp로 제외하고 뒤짚어 쓰면서 행렬을 회전시키고,   
최소값을 뽑아내었다.   

```
import java.util.Arrays;
class Solution {
    static int[][] board;
    static int n;
    static int m;
    public int[] solution(int rows, int columns, int[][] queries) {
        int[] answer = new int[queries.length];
        int idx = 0;
        n = rows;
        m = columns;
        board = new int[rows][columns];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns; j++){
                board[i][j] = (i*columns + j + 1);
            }
        }
        //System.out.println(Arrays.deepToString(board));
        for (int[] query : queries) {
            int startY = query[0], startX = query[1];
            int endY = query[2], endX = query[3];
            
            answer[idx++] = rotation(startY, startX, endY, endX);
        }
        return answer;
    }
    
    public int rotation(int startY, int startX, int endY, int endX) {
        int min = n*m;
        // 오른쪽으로
        int tempUp = board[startY-1][endX-1];
        for (int i = endX-1; i > startX-1; i--) {
            board[startY-1][i] = board[startY-1][i-1];
            min = Math.min(board[startY-1][i], min);
        }
        //System.out.println(Arrays.toString(board[startY-1]));
        // 밑으로
        int tempDown = board[endY-1][endX-1];
        for (int i = endY-1; i > startY; i--) {
            board[i][endX-1] = board[i-1][endX-1];
            min = Math.min(board[i][endX-1], min);
        }
        board[startY][endX-1] = tempUp;
        // for (int i = startY-1; i < endY; i++) {
        //     System.out.println(board[i][endX-1]);
        // }
        // 왼쪽으로
        int tempLeft = board[endY-1][startX-1];
        for (int i = startX-1; i < endX-1; i++) {
            board[endY-1][i] = board[endY-1][i+1];
            min = Math.min(board[endY-1][i], min);
        }
        board[endY-1][endX-2] = tempDown;
        //System.out.println(Arrays.toString(board[endY-1]));
        // 윗쪽으로
        for (int i = startY-1; i < endY-1; i++) {
            board[i][startX-1] = board[i+1][startX-1];
            min = Math.min(board[i][startX-1], min);
        }
        board[endY-2][startX-1] = tempLeft;
        // for (int i = startY-1; i < endY; i++) {
        //     System.out.println(board[i][startX-1]);
        // }
        min = Math.min(min, tempUp);
        min = Math.min(min, tempDown);
        min = Math.min(min, tempLeft);
        //System.out.println(Arrays.toString(board[startY-1]));
        return min;
    }
}
```
