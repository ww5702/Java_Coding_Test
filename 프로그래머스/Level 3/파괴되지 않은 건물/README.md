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
누적합을 이용해서 풀이하는것이었다.   
0,0에서부터 2,3까지 3을 더하는것이라면
0 0 0 0 0  
0 0 0 0 0  
0 0 0 0 0  
0 0 0 0 0  
일때   
3 0 0 0 -3  
0 0 0 0 0  
0 0 0 0 0  
-3 0 0 0 3  
와 같이 만들어준다.   
그리고 모든 공격 방어들을 더하거나 뺀 뒤   
오른쪽으로 누적합,   
3 3 3 3 0   
0 0 0 0 0   
0 0 0 0 0  
-3 -3 -3 -3 0   
그리고 아래로 누적합을 진행한다.   
3 3 3 3 0   
3 3 3 3 0   
3 3 3 3 0   
0 0 0 0 0   
그러면 최종적으로 0,0 에서 2,3까지 3을 더한값이 된다.   
   
좋아요를 가장 많이 받은 풀이도 누적합으로 풀이를 진행하였다.   

```
import java.util.Arrays;
class Solution {
    public int solution(int[][] board, int[][] skill) {
        int answer = 0;
        int[][] sumArr = new int[board.length][board[0].length];
        for (int i = 0; i < skill.length; i++) {
            /*
            (y1,x1) 에 n을 (y1,x2+1)에 -n을
            (y2+1,x1) 에 -n을 (y2+1,x2+1)에 n을
            */
            int[] command = skill[i];
            int type = command[0];
            int y1 = command[1], x1 = command[2];
            int y2 = command[3], x2 = command[4];
            int value = command[5];
            if (type == 1) {
                sumArr[y1][x1] -= value;
                if (x2 + 1 < board[0].length) {
                    sumArr[y1][x2+1] += value;
                }
                if (y2 + 1 < board.length) {
                    sumArr[y2+1][x1] += value;
                }
                if (x2+1 < board[0].length && y2+1 < board.length) {
                    sumArr[y2+1][x2+1] -= value;
                }
            } else {
                sumArr[y1][x1] += value;
                if (x2 + 1 < board[0].length) {
                    sumArr[y1][x2+1] -= value;
                }
                if (y2 + 1 < board.length) {
                    sumArr[y2+1][x1] -= value;
                }
                if (x2 + 1 < board[0].length && y2 + 1 < board.length) {
                    sumArr[y2+1][x2+1] += value;
                }
            }
            
        }
        
        for (int i = 0; i < board.length; i++) {
            int sum = sumArr[i][0];
            for (int j = 1; j < board[0].length; j++) {
                sum += sumArr[i][j];
                sumArr[i][j] = sum;
            }
        }
        
        
        for (int i = 0; i < board[0].length; i++) {
            int sum = sumArr[0][i];
            for (int j = 1; j < board.length; j++) {
                sum += sumArr[j][i];
                sumArr[j][i] = sum;
            }
        }
        
        // for (int i = 0; i < board.length; i++) {
        //    System.out.println(Arrays.toString(sumArr[i]));
        // }
        
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                answer += sumArr[i][j] + board[i][j] <= 0 ? 1 : 0;
            }
        }
        //System.out.println(answer);
        
        
        return (board.length * board[0].length) - answer;
    }
}
```
