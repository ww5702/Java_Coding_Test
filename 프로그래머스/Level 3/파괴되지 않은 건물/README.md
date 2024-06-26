그냥 빼고 더하는걸로는 효율성테스트를 통과하지 못한다.   

```
import java.util.Arrays;
class Solution {
    public int solution(int[][] board, int[][] skill) {
        int answer = 0;
        for (int i = 0; i < skill.length; i++) {
            int[] command = skill[i];
            int type = command[0];
            int y1 = command[1], x1 = command[2];
            int y2 = command[3], x2 = command[4];
            int value = command[5];
            if (type == 1) {
                for (int y = y1; y <= y2; y++) {
                    for (int x = x1; x <= x2; x++) {
                        board[y][x] -= value;
                    }
                }
            } else {
                for (int y = y1; y <= y2; y++) {
                    for (int x = x1; x <= x2; x++) {
                        board[y][x] += value;
                    }
                }
            }
            
            
            
        }
        
        // for (int i = 0; i < board.length; i++) {
        //    System.out.println(Arrays.toString(board[i]));
        // }
        
        for (int i = 0; i < board.length; i++) {
            answer += Arrays.stream(board[i]).filter(n -> n <= 0).count();
        }
        
        
        return (board.length * board[0].length) - answer;
    }
}
```
