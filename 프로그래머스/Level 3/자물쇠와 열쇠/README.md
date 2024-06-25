구현문제이다.   
key + Lock + key 크기로 새로운 배열을 준비한다.   
key를 맨 위에서부터 lock + key - 2 크기까지 순환하면서 더해본다.   
가운데 lock 배열부분이 전부 1이라면 자물쇠가 열린다.   
한번 순환한다음 key를 90도 회전하는 함수를 더해준다.   
이렇게 4번 반복해서 자물쇠가 열리지 않으면 false이다.   

```
import java.util.Arrays;
class Solution {
    static int n;
    static int m;
    public boolean solution(int[][] key, int[][] lock) {
        boolean answer = true;
        n = lock.length;
        m = key.length;
        //System.out.println(lock.length + (key.length*2) - 2);
        int[][] board = new int[n+(m*2)-2][n+(m*2)-2];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                board[i+m-1][j+m-1] = lock[i][j];
                //System.out.println((i+m-1)+" "+(j+m-1));
            }
        }
        for (int t = 0; t < 4; t++) {
            for (int i = 0; i <= n+m-2; i++) {
                for (int j = 0; j <= n+m-2; j++) {
                    //System.out.println(i+" "+j);
                    
                    int[][] tempBoard = new int[board.length][board[0].length];

                    for(int q = 0; q < board.length; q++){
                        for(int w = 0 ; w < board[0].length; w++){
                            tempBoard[q][w] = board[q][w];
                        }
                    }
                    
                    // 열쇠 더하기
                    for (int y = 0; y < m; y++) {
                        for (int x = 0; x < m; x++) {
                            tempBoard[i+y][j+x] += key[y][x];
                        }
                    }
                    
                    // 열쇠 확인하기
                    if (check(tempBoard)) {
                        return true;
                    }
                    // for (int a = 0; a < 7; a++) {
                    //         System.out.println(Arrays.toString(tempBoard[a]));
                    //     }
                    //     System.out.println();
                }
                
            }
            key = rotaion(key);
        }
        
        return false;
    }
    public boolean check(int[][] board) {
        boolean isOk = true;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i+m-1][j+m-1] != 1) {
                    isOk = false;
                    break;
                }
            }
        }
        return isOk;
    }
    public int[][] rotaion(int[][] key) {
        int nn = key.length;
        int mm = key[0].length;
        int[][] rotate = new int[mm][nn];

        for (int i = 0; i < rotate.length; i++) {
            for (int j = 0; j < rotate[i].length; j++) {
                rotate[i][j] = key[nn-1-j][i];
            }
        }

        return rotate;
    }
}
```
좋아요를 가장 많이 받은 풀이이다.   
풀이 방식은 같고 가독성을 위해 함수를 더 많이 사용했다.   
```
lass Solution {

    public int[][] roll(int[][] mat)
    {
        int[][] temp = new int[mat.length][mat.length];

        for (int i = 0; i < mat.length; i++)
        {
            for (int j = 0; j < mat.length; j++)
            {
                temp[i][j] = mat[mat.length - j - 1][i];
            }
        }

        return temp;
    }

    public int[][] move(int[][] key, int length, int row, int col)
    {
        int[][] temp = new int[length][length];

        for (int i = 0; i < key.length; i++)
        {
            for (int j = 0; j < key.length; j++)
            {
                if (i + row >= 0 && i + row < length && j + col >= 0 && j + col < length)
                {
                    temp[i + row][j + col] = key[i][j];
                }
            }
        }

        return temp;
    }

    public boolean same(int[][] key, int[][] lock)
    {
         for (int n = 0; n < lock.length; n++)
        {
            for (int m = 0; m < lock.length; m++)
            {
                if ((key[n][m] ^ lock[n][m]) == 0)
                {
                    return false;
                }
            }
        }
        return true;
    }

    public boolean check(int[][] key, int[][] lock)
    {
        int[][] mat = new int[lock.length * 2 - 1][lock.length * 2 - 1];

        for (int i = (1 - key.length); i < lock.length; i++)
        {
            for (int j = (1 - key.length); j < lock.length; j++)
            {
                int[][] temp = move(key, lock.length, i, j);
                if (same(temp, lock))
                {
                    return true;
                }
            }
        }

        return false;
    }

    public boolean solution(int[][] key, int[][] lock) {
        boolean answer = false;

        for (int i = 0; i < key.length; i++)
        {
            if (check(key, lock))
            {
                return true;
            }

            key = roll(key);
        }



        return answer;
    }
}

```
