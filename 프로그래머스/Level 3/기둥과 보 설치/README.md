기둥과 보를 따로 2차원배열로 저장해준다.   
그리고 설치가 가능한지 불가능한지 각각 비교해준다.   

```
import java.util.*;
class Solution {
    static boolean[][] Gidong;
    static boolean[][] Bo;
    public int[][] solution(int n, int[][] build_frame) {
        
        Gidong = new boolean[n+1][n+1];
        Bo = new boolean[n+1][n+1];
        
        int cnt = 0;
        for (int[] b_frame : build_frame) {
            int x = b_frame[0];
            int y = b_frame[1];
            int type = b_frame[2];
            int install = b_frame[3];
            
            // 설치인지 삭제인지
            if (install == 0) {
                // 기둥인지 보인지
                if (type == 0) {
                    Gidong[x][y] = false;
                    
                    if (canDelete(n)) {
                        cnt -= 1;
                    } else {
                        Gidong[x][y] = true;
                    }
                } else {
                    Bo[x][y] = false;
                    
                    if (canDelete(n)) {
                        cnt -= 1;
                    } else {
                        Bo[x][y] = true;
                    }
                }
            } else if (install == 1) {
                // 기둥인지 보인지
                if (type == 0) {
                    if (checkGidong(x,y)) {
                        Gidong[x][y] = true;
                        cnt += 1;
                    }
                } else {
                    if (checkBo(x,y)) {
                        Bo[x][y] = true;
                        cnt += 1;
                    }
                }
            }
        }
        int[][] answer = new int[cnt][3];
        int idx = 0;
        for (int i = 0; i <= n; i++) {
            for (int j = 0; j <= n; j++) {
                if (Gidong[i][j]) {
                    answer[idx][0] = i;
                    answer[idx][1] = j;
                    answer[idx][2] = 0;
                    idx += 1;
                }
                
                if (Bo[i][j]) {
                    answer[idx][0] = i;
                    answer[idx][1] = j;
                    answer[idx][2] = 1;
                    idx += 1;
                }
            }
        }
        return answer;
    }
    // 기둥 검증
    // 바닥 위에 (y == 0)
    // 기둥 위인가 (board[0][y-1][x] == 1)
    // 보의 한쪽 끝인가 (맵을 벗어나지 않고)
    // board[1][y][x] == 1 || x-1 >= 0 && board[1][y][x-1] == 1
    public boolean checkGidong(int x, int y) {
        // 바닥 위에 / 기둥 위인가 / 보의 한쪽 끝인가
        if (y == 0) return true;
        else if (Gidong[x][y-1] && y > 0) return true;
        else if (x > 0 && Bo[x-1][y] || Bo[x][y]) return true;
        return false;
    }
    
    // 보 검증
    // 한쪽 끝이 기둥인가 (벽을 넘지 않고)
    // 양쪽 끝이 다른 보와 연결되어있는가 (벽을 넘지 않고)
    public boolean checkBo(int x, int y) {
        // 한쪽 끝에 기둥이 있는가 / 양쪽 끝이 다른 보와 연결되어있는가
        if (y > 0 && Gidong[x][y-1] || Gidong[x+1][y-1]) return true;
        else if (x > 0 && Bo[x-1][y] && Bo[x+1][y]) return true;
        return false;
    }
    
    //삭제
    public boolean canDelete(int n) {
        for (int i = 0; i <= n; i++) {
            for (int j = 0; j <= n; j++) {
                // 기둥이 해당위치에 있을 수 없다면 불가
                if (Gidong[i][j] && !checkGidong(i,j)) return false;
                else if(Bo[i][j] && !checkBo(i,j)) return false;
            }
        }
        
        return true;
    }
}
```

좋아요를 가장 많이 받은 풀이 또한 위와 같았다.   
구현 문제이다.   
