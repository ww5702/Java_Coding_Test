```
import java.util.Stack;
import java.util.Arrays;
class Solution {
    public int solution(int[][] board, int[] moves) {
        int answer = 0;
        Stack<Integer> result = new Stack<>();
        
        for (int move : moves) {
            for (int i = 0; i < board.length; i++) {
                
                if (board[i][move-1] != 0) {
                    if (result.isEmpty()) {
                        result.push(board[i][move-1]);
                        board[i][move-1] = 0;
                        break;
                    }
                    
                    if (result.peek() == board[i][move-1]) {
                        answer += 2;
                        result.pop();
                    } else 
                        result.push(board[i][move-1]);
                        board[i][move-1] = 0;
                        break;
                    }
                }
            }
        return answer;
    }
}
```
