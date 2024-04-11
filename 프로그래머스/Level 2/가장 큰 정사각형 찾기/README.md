0	1	1	1   
1	1	1	1   
1	1	1	1   
0	0	1	0   
일때 정사각형이 전부 1이라면 2를 반환시켜준다.   
0 1 1 1   
1 2 2 2   
1 2 3 3   
0 0 1 1   
이 된다.   
여기서 3이 가장 큰 수이고,   
3x3인 9가 가장 큰 정사각형이 된다.   
기본 answer을 1로 만들어 board크기가 1인 경우를 대비하려 했지만   
정답이 0인 경우도 있어 0으로 초기화하고 1인 경우는 따로 만들어준다.   
```
class Solution
{
    public int solution(int [][]board)
    {
        int answer = 0;
        if (board.length == 1) {
            return 1;
        } else {
            for (int i = 1; i < board.length; i++) {
                for (int j = 1; j < board[0].length; j++) {
                    if (board[i][j] != 0) {
                        board[i][j] = board[i][j] + Math.min(board[i-1][j], Math.min(board[i-1][j-1], board[i][j-1]));
                        answer = Math.max(board[i][j], answer);
                    }
                //System.out.println(i+" "+j);
                }
            }
        }
        
        
        return answer*answer;
    }
}
```
